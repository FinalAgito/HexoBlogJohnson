---
title: C++设计模式（二）：单例模式
date: 2016-07-31 11:19:49
categories: C++设计模式
tags: C++
---
# 一.什么是单例模式？
　　这次我们介绍的是单例模式，也是创建型模式的一种，这应该是最为简单的一种，那么，什么是单例模式呢？
所谓的单例模式，是我们在运行程序的时候，有些实例，在程序中只要存在一个就足够了，如果我们每次进行某项操作都会创建一个实例，则这会对计算机的资源和空间造成较大的浪费，这是我们不愿意看到的。
　　就比如我们之前所说的工厂模式，我们当然希望系统当中只存在、也只可以存在一个工厂，如果我们在每调用一个功能的时候就创建一个工厂，就会对计算机的资源造成极大的浪费，我们无法对工厂实例进行有效的操作（如果需要的话）。
　　而单例模式，就是用来保证我们所需要的对象在程序运行中只存在1个而存在的（其实你可以用添加一个计数属性的方法让它能够实例化为有限个，但是实际上我们一般并不需要这样的办法）。
　　其意图是保证一个类仅有一个实例，并提供一个访问它的全局访问点（你也许可以称它为接口），该实例被所有程序模块共享。
# 二.单例模式
　　就像我们前面所说，单例模式，是为了保证我们所需要的对象在程序运行中只存在1个。那么它究竟做了什么操作？
　　实际上，单例模式的步骤非常简单。
　　单例模式的主要操作就是将一个类实例化之前，首先对当前程序进行确认，看现在的程序当中是否已经存在了一个实例化的对象，如果存在，则我们直接将这个对象的引用或者指针返回，即获取到当前存在的这个对象，反之，则创建这个对象，从而保证该种类的对象在程序中只存在一个。
也许我应该先上段代码？
```
//这是我们所要求全局只能存在一个的类
class CSingleton
{
private:
	CSingleton(){};
	static CSingleton *m_pInstance;//静态指针

public:
	virtual ~CSingleton(){};
	static CSingleton*	GetInstance()
	{
		if(m_pInstance == NULL)//判断对象是否存在
			m_pInstance = new CSingleton();
		return m_pInstance;
	}
};
************调用**************
CSingleton* CSingleton::m_pInstance = NULL;
int _tmain(int argc, _TCHAR* argv[])
{
	CSingleton *p1 = CSingleton::GetInstance();
	CSingleton *p2 = p1->GetInstance();
	return 0;
}

```
　　如你所想，不难，确实可以称的上是最容易的设计模式了，而我将它作为第二个设计模式来讲，除了它简单以外，其实还有一个原因，就是它经常和工厂模式结合使用
那么你也猜到我下面要做一些扩展了对不？
没错，那就是------
# 三.结合了单例模式的简单工厂模式
　　实际上我们还有另外一个例子可以使用这个单例的概念，比如我们点击一次按钮，创建一个窗口，那么如果我再按一次，如果并非单例模式，那么我每按一次都会产生一个窗口，到最后想像一下满屏窗口的场景......嗯，还是单例模式好。
　　那么我们来看一看他们的UML图（请原谅我用上次的例子炒现成的）：
![图 3-1 结合了单例模式的简单工厂模式UML示例图](\images\C++designer\SingletonMode\Singleton.png)
```
//运算类
class Operation{
private:
	
	double A;//第一个数
    double B;//第二个数
public:
	Operation(){};
	virtual ~Operation(){};
	bool SetA(double a)//设定A
	{
		this->A = a;
		return true;
	};
	
	bool SetB(double b)//设定B
{
		this->B = b;
		return true;
	};
	double GetA()//获得A
	{
		return this->A;
	};
	double GetB()//获得B
	{
		return this->B;
	};
	virtual double GetResult() = 0;
	

};
//相加类，在此处我们继承了运算类
class Sub :public Operation
{
public:
	Sub(){};
	virtual ~Sub(){};
	double GetResult()
	{
		return GetA() + GetB();
	};
};
//相减类，同样继承了运算类
class Dec :public Operation
{
public:
	Dec(){};
	virtual ~Dec(){};
	double GetResult()
	{
		return GetA() - GetB();
	};
};
//工厂类，在此我们不用其他更复杂的工厂形式了，直接用简单的
class Factory
{

private:
//注意这里是一个关键点，我们将构造函数归为private一类，让从外部无法单独实例化它，而必须通过下面的Create函数
	Factory(){};
	static Factory* Factory_Instance;
public:
//没错就是它
	static Factory * Create()
	{
		if (Factory_Instance == NULL)
			Factory_Instance = new Factory();
		return Factory_Instance;
	}
	
	Operation *CreateProject(string type)
	{
		if (type=="Sub")
		return new Sub();
		if (type == "Dec")
			return new Dec();
		return NULL;
	};
};
**************主函数调用*****************
//静态指针要在此处实例化
 Factory* FactoryChild :: Factory_Instance = NULL;
int _tmain(int argc, _TCHAR* argv[])
{
	Factory* Test =  Factory :: Create();
   Operation *p1 =	Test->CreateProject("Sub");
   p1->SetA(4);
   p1->SetB(8);
   cout<<p1->GetResult()<<endl;
   Factory* Test2 = Factory :: Create();
   Operation *p2 = Test->CreateProject("Dec");
   cout << p2->GetResult();
//结果为12
}
```
# 四.注意点
　　1,构造函数不能被继承，单例模式中必须将构造函数设置为私有，将析构函数设置为公有虚函数
　　2,可以在单例模式中再调用单例，通过对象引用和对象指针实现虚函数的多态，公有继承基类有的虚函数，派生类的成员函数不使用virtual也是虚函数，但是函数内部具体调用的函数又是另外一个概念了，良好的做法就是在派生类中也使用关键字virtual
# 五.单例模式的优缺点
优点：
1.减少了时间和空间的开销（new实例的开销）。
2.提高了封装性，使得外部不易改动实例。
缺点：
1.由于单例模式中没有抽象层，因此单例类的扩展有很大的困难。
2.单例类的职责过重，在一定程度上违背了“单一职责原则”。
3.滥用单例将带来一些负面问题，如为了节省资源将数据库连接池对象设计为的单例类，可能会导致共享连接池对象的程序过多而出现连接池溢出。如果实例化的对象长时间不被利用，系统会认为是垃圾而被回收，这将导致对象状态的丢失。
以上的缺点都是一些滥用单例模式带来的错误，但是说实在的，你总有要用到它的时候，不过要谨慎使用就是了（笑）。
