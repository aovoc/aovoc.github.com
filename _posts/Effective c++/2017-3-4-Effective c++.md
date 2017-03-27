---
layout: post
category : Effective c++
tagline: ""
tags : [c++]
---
{% include JB/setup %}


#让自己习惯C++
##Rule 01: 视c++为一个语言联邦
次语言：c、Object-Oriented c++、Template C++、 STL        


##Rule 02: 尽量以const、enums、inline 代替 #define
编译器代替预处理器      
/#define 不重视定义域，不提供封装性 

	enum{NumTurns = 5};  //"the enum hack" 
	
	tempplate<typename T>
	inline void callWithMax(const T&a, const T& b){
		f(a>b ? a : b); // f：调用函数
	}
	

##Rule 03: 尽可能地使用const
const 出现在*号左边，被指物为常量， 出现在*号右边，指针自身为常量
const_iterator 
令函数返回一个常量值，降低因客户错误而造成的意外，而又不至于放低安全性和高效性。

	Rational a, b, c;
	if(a*b = c) //comparison error
	
将某些东西声明为const 可帮助编译器检测出错误语法
令non-const 版本调用const版本可以避免代码重复。


#Rule 04: 确定对象被使用前已先被初始化

使用成员初始化列表来代替赋值操作。
设为default，成员初始化列表指定为空。

C++成员初始化次序
base classes > derived class 
class 成员变量以声明的次序被初始化

晦涩错误：成员变量的初始化带有次序性，例：array 指定大小


C++对于定义在不同文件中的non-local static 对象的初始化顺序没有明确的顺序。
解决方法：通过函数调用（返回一个reference指向local static）代替non-local static的访问。


#构造/析构/赋值运算
##Rule 05: 了解C++默默编写并调用了哪些函数
	
	class Empty{};
	//is the same as
	class Empty{
	public:
		Empty(){...};                        //default 构造函数
		~Empty(){...};                       //析构函数
		Empty(const Empty& rhs){...};        //copy函数
		Empty &operator =(const Empty& rhs){...};      //copy assignment
	}
	
	
	
##Rule 06: 若不想使用编译器自动生成的函数，就该明确拒绝

	class Uncopyable{
	protected:
		Uncopyable(){};
		~Uncopyable(){};
	private:
		Uncopyable(const Uncopyable&)
		Uncopyable & operator =(const Uncopyable &);
	}
	
	class HomeForSale: private Uncopyable{
	}
	
##Rule 07:为多态基类声明virtual析构函数
当derived class 对象经由一个base class 指针被删除，而该base class 带有一个non-virtual 析构函数，其结果未有定义，实际执行时通常发生的是对象的derived 成分没有被销毁。造成资源泄露、败坏的数据结构等。
若class不含virtual函数，意味着不是一个base class,不应将析构函数设为virtual。
实现virtual函数对象需要实现vptr,与其它语言不再具有移植性。
std::string 的析构函数是non-virtual。
不要企图继承标准容器或者带有non-virtual析构函数的class。
pure virtual 函数导致abstract classes。不能被实体化。
析构函数的运作方式：最深层的class的析构函数最先被调用。然后是其每一个上层的base class。
	
##Rule 08:别让异常逃离析构函数
析构函数绝对不要吐出异常。如果一个被析构函数调用的函数可能抛出异常，析构函数应该捕捉异常并吞下或者结束程序。
如果需要对异常做出反应，那么应该提供一个普通函数执行该操作。


##Rule 09:绝不在构造和析构函数中调用virtual函数
会带来意想不到的结果。与java和c#不同的地方。
 调用virtual函数会下降到derive class 阶层。使用对象内部尚未初始化部分=危险
 
##Rule 10:令operator= 返回一个 reference to *this

##Rule 11: 在operator=中处理“自我赋值”
	
	Widget& Widget::operator=(const Widget& rhs){
		Widget tmp(rhs);
		swap(rhs, tmp);
		return *this;
	}
	
##Rule 12:复制对象时勿忘其每一个成分
为derive class 撰写copy 函数时要复制其base class 成分。那些成分往往是private，应调用base class 相应的函数进行复制。

不要尝试以某个copying函数实现另一个copying函数，应该将共同的机能放在第三个函数中。

#资源管理
##Rule 13:以对象管理类型资源

	void f()
	{
		std::auto_ptr<Investment> pInv(createInvestment());
		...
	}

RAII
获得资源后立即放进管理对象。
管理对象运行析构函数确保资源释放。

auto_ptr被销毁时自动删除它的所指之物，勿让多个auto_ptr指向同一个对象。对象被删除多次 = 未定义行为

auto_ptr不寻常的性质：通过copy、copy assignment 复制他们，它们会变成null,而复制所得的指针将取得资源的唯一拥有权。

引用计数型智慧指针
	
	void f()
	{
		...
		std::tr1::share_ptr<Investment> pInv(createInvestment());
		...
	}

在c++11引入share_ptr


##Rule 14:在资源管理类中小心copy行为


##Rule 15:在资源管理类中提供对原始资源的访问


##Rule 16:成对使用new 和delete时要采取相同形式

待续....
