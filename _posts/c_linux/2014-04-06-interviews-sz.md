---
layout: post
title: Interviews
category: c_linux
tags: interviews
keywords: interview
description: 2014
---

### 1、map 内有为结构体的键值，怎么使用

### 2、获取共享内存的函数：shmget、shmat、shmdt、shmctl

### 3、strstr(*str1, *str2)      ：：实现从字符串str1中查找是否有字符串str2，如果有，从str1中的str2位置起，返回str1中str2起始位置的指针，如果没有，返回null。

### 4、函数库调用和系统调用区别:
函数库调用是语言或应用程序的一部分，而系统调用是操作系统的一部分。
用户应用程序访问并使用内核所提供的各种服务的途径即是系统调用。在内核和用户应用程序相交界的地方，内核提供了一组系统调用接口，通过这组接口，应用程序可以访问系统硬件和各种操作系统资源。 

### 1.系统调用是为了方便应用使用操作系统的接口，而库函数是为了方便人们编写应用程序而引出的，比如你自己编写一个函数其实也可以说就是一个库函数。

### 2.系统调用可以理解为内核提供给我们在用户态用的接口函数，可以认为是某种内核的库函数。

### 3.read就是系统调用,而fread就是C标准库函数.
※函数库调用 VS系统调用
| 函数库调用        | 系统调用 |
| --------  |  -----:|
| 在所有的ANSI C编译器版本中，C库函数是相同的     | 各个操作系统的系统调用是不同的 |
| 它调用函数库中的一段程序（或函数）	        |   它调用系统内核的服务   |
| 与用户程序相联系        |    是操作系统的一个入口点    |
|在用户地址空间执行|在内核地址空间执行|
|它的运行时间属于“用户时间”	| 它的运行时间属于“用户时间”	|
|属于过程调用，调用开销较小	   |   需要在用户空间和内核上下文环境间切换，开销较大|
|在C函数库libc中有大约300个函数	  |  在UNIX中大约有90个系统调用  |
|典型的C函数库调用：system fprintf malloc  | 典型的系统调用：chdir fork write brk|

系统调用和函数库的关系：
系统调用通过软中断int0x80从用户态进入内核态。
函数库中的某些函数调用了系统调用。
函数库中的函数可以没有调用系统调用，也可以调用多个系统调用。
编程人员可以通过函数库调用系统调用。
高级编程也可以直接采用int0x80进入系统调用，而不必通过函数库作为中介。
如果是在核心编程，也可以通过int0x80进入系统调用，此时不能使用函数库。因为函数库中的函数是内核访问不到的。
printf是标准输出流的输出函数，用来向屏幕这样的标准输出设备输出，而fprintf则是向文件输出，将输出的内容输出到硬盘上的文件或是相当于文件的设备上
printf是有缓冲的输出，fprintf没有缓冲
fprintf()传送输出到一个流中的函数

### 5、new和malloc的区别：：
1 malloc与free是C++/C语言的标准库函数，new/delete是C++的运算符。它们都可用于申请动态内存和释放内存。
2 对于非内部数据类型的对象而言，光用maloc/free无法满足动态对象的要求。对象在创建的同时要自动执行构造函数，对象在消亡之前要自动执行析构函数。由于malloc/free是库函数而不是运算符，不在编译器控制权限之内，不能够把执行构造函数和析构函数的任务强加于malloc/free 3 3 因此C++语言需要一个能完成动态内存分配和初始化工作的运算符new，以一个能完成清理与释放内存工作的运算符delete。注意new/delete不是库函数。
4 C++程序经常要调用C函数，而C程序只能用malloc/free管理动态内存。
5 new可以认为是malloc加构造函数的执行。new出来的指针是直接带类型信息的。而malloc返回的都是void指针。
### 6、考察 模板！~
7、C++预处理指令
    #includ
    #define
    #undef
    #pragma
    #import
    #error
    #line
    #ifdef
    #ifndef
    #if
    #else
    #elif
    #endif
8、逻辑运算符《关系运算符《算术运算符  
例如：9>3+4&&7
先算3+4  再判断9是不是大于7，再&&
### 9、为什么基类的析构函数是虚函数？
在实现多态时，当用基类操作派生类，在析构时防止只析构基类而不析构派生类的状况发生。
当基类指针指向new生成的派生类对象时，delete基类指针时派生类部分没有释放掉而造成释放不彻底现象，需要虚析构函数。
10、volatile是一个类型修饰符。理解volatile~!
11、虚函数 理应函数返回值和参数个数类型都一样才好统一接口。
12、数组和vector 的区别：
：数组是内置类型，运行期大小不可改变，存储在栈区；vector是STL中类模板，运行期可动态改变长度，存储在堆区；

### 第七大道

算法：1、N进制数转化成M进制数
     2、高精度数的乘法
     *3、字符串匹配
      1、求n个数中第K大数：：     快排和堆排
      2、归并排序和快排的区别
时间复杂度一样；如果比较无序快排比较快，如果基本有序归排比较快，归并排序是稳定的，

|------  |  堆排序     |    归并排序  |  快速排序  |
|:------ | :--------:  | :------:  | :----:      |
|最坏时间|  O(nlogn)   |  O(nlogn) |   O(n^2)    |
|最好时间|  O(nlogn)   |   O(nlogn) |  O(nlogn)  |
|平均时间|  O(nlogn)   |    O(nlogn) | O(nlogn） |

3、MVC分别代表什么：：：MVC全名是Model  View  Controller，
是模型(model)－视图(view)－控制器(controller)的缩写，一种软件设计典范

4、哈希表处理冲突，求线性探测法求平均长度（线性再散列的公式为：Hi=（H(key)+di）% m）
原题：     已知一个线性表（38，25，74，63，52，48），假定采用散列函数h(key)=key%7计算散列地址，并散列存储在散列表A[0..6]中，若采用线性探测方法解决冲突，

 则 在该散列表上进行等概率成功查找的平均查找长度为_____.
 A.1.5 B.1.7 C.2.0 D.2.3
 分析：利用该散列函数散列存储结果为
 68|48 | |38|25|74|52
 位置 0 1 2 3 4 5 6
 平均查找长度=总的查找次数/元素数=（1*3+2*1+3*1+4*1）/6=2.0
 参考答案：C

5、求x=A+B*(C-D) / E 后缀表达式:
算法描述： 
    将中缀表达式转换为等价的后缀表达式的过程要使用一个栈放“（”，具体可以按照下面的方式进行。 
    （1）从左到右依次扫描中缀表达式的每一个字符，如果是数字字符和圆点“.”则直接将它们写入后缀表达式中。 
    （2）如果遇到的是开括号“（”，则将它们压入一个操作符栈（不需要与栈顶操作符相比较），它表明一个新的计算层次的开始，在遇到和它匹配的闭括号“）”时，将栈中的元素弹出来并放入后缀表达式中，直到栈顶元素为“(”时，将栈顶元素“（”弹出（不需要加入后缀表达式），表明这一层括号内的操作处理完毕。
    （3）如果遇到的是操作符，则将该操作符和操作符栈顶元素比较： 
        1、当所遇到的操作符的优先级小于或等于栈顶元素的优先级时，则取 出栈顶元素放入后缀表达式，并弹出该栈顶元素，反复执行直到当前操作符的优先级大于栈顶元素的优先级小于；
        2、当所遇到的操作符的优先级大于栈顶元素的优先级的时则将它压入栈中。 
    （4）重复上述步骤直到遇到中缀表达式的结束符标记“#”，弹出栈中的所有元素并放入后缀表达式中，转换结束


6、99！ 总共有几个零
   分析：
        一般类似的题目都会蕴含某种规律或简便方法的阶乘末尾一个零表示一个进位，则相当于乘以10
而10 是由2*5所得，在1~100当中，可以产生10的有：0 2 4 5 6 8结尾的数字，显然2是足够的，因为4、6、8当中都含有因子2，所以都可看当是2，那么关键在于5的数量了那么该问题的实质是要求出1~100含有多少个5由特殊推广到一般的论证过程可得：
        每隔5个，会产生一个0，比如 5， 10 ，15，20.。。 
        每隔 5×5 个会多产生出一个0，比如 25，50，75，100 
        每隔 5×5×5 会多出一个0，比如125.
        所以99！末尾有多少个零为：
         99/5+99/25=19+3=22
        那么1000！末尾有多少个零呢？同理得：
       1000/5+1000/25+1000/125=200+40+8=248
到此，问题解决了，但我们在学习过程中应当学会发散思维、举一反三

7、 HTTP：：超文本传输协议 (HTTP-Hypertext transfer protocol) 是一种详细规定了浏览器和万维网服务器之间互相通信的规则，通过因特网传送万维网文档的数据传送协议。
ARP，（Address Resolution Protocol）一般指地址解析协议

DNS 是域名系统 (Domain Name System) 的缩写，是因特网的一项核心服务，它作为可以将域名和IP地址相互映射的一个分布式数据库，能够使人更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串。

TCP：：Transmission Control Protocol 传输控制协议TCP是一种面向连接（连接导向）的、可靠的、基于字节流的传输层（Transport layer）通信协议

TCMP：：（Internet Control Message Protocol）Internet控制报文协议。它是TCP/IP协议族的一个子协议，用于在IP主机、路由器之间传递控制消息

IP：：：IP是英文Internet Protocol（网络之间互连的协议）的缩写，中文简称为“网协”，也就是为计算机网络相互连接进行通信而设计的协议

1、htonl()::htonl就是把本机字节顺序转化为网络字节顺序,
h---host 本地主机
to  就是to 了
n  ---net 网络的意思
l 是 unsigned long
如果一个数以小尾顺序存储，经htonl函数调用后这个数的高地位字节会完全颠倒过来成为一个新的数。这个新的数在机器内部其实还是以小尾顺序存储的，但是相对于原来的数而言相当于是变成大尾顺序的了。
long型的0x40写完整为:0x 00 00 00 40，共四个字节，调用htonl后四个字节颠倒顺序，为0x 40 00 00 00。
2、加入异常判断代码：：
3、新建线程函数CreateThread
新建进程函数CreateProcess
4、函数指针
5、模板
6、

### 与struct相关的宏定义 ---今Tencent笔试用到的
获取成员变量的偏移以及通过成员变量的地址获取struct的起始地址
获取成员变量的偏移以及通过成员变量的地址获取struct的起始地址
1. 获取成员变量的偏移。
 #define offset_of(type, field) ( (unsigned int)&(((type *)(0))->field) ) 
简单解释一下这个宏：

	//如果我们定义一个struct:
	typedef struct{
	  int a;
	  int b;
	} A;

那么offset_of(A, b)就会输出b相对于起始地址的偏移。
& -- 这是取地址符号，表示获取当前变量的地址。
0 -- 这是这个宏中最核心的地方。我们知道，对于一个struct, 比如说上面的A,  &A->b代表了b的地址， 如果我们想得到b相对于A的偏移，那么&A->b - &A就可以得到。
但如是&A就是0呢。那么&A->b不就是偏移了吗？

2、如果已知成员变量的地址，那我们也可以轻松得获取该成员所在结构体的首地址。代码如下：
`#define container_of(ptr, type, field) (type *)((char *)ptr - offset_of(type, field))`  
我们只需要把该成员变量的地址减去你相对于首地址的偏移，不就是该结构体的首地址了么？
结出一个完整的实例：

	// testConsole.cpp : Defines the entry point for the console application.  
	
	#include "stdafx.h"  
	#include <time.h>  
	#include <stdio.h>  
	#include <stdlib.h>  
	  
	#define offset_of(type, field) ( (unsigned int)&(((type *)(0))->field) )  
	#define container_of(ptr, type, field) (type *)((char *)ptr - offset_of(type, field)) 
	typedef struct{  
	    int     a;  
	    int     b;  
	    char    c;  
	    int     d;  
	}package_t;  
	  
	int main()  
	{  
	    package_t pkg;  
	    int *p;  
	  
	    p = (int *)&pkg.d;  
	    printf("offset of 'd' is %d.\n", offset_of(package_t, d));  
	    printf("The addr of pkg = 0x%x.\n", &pkg);  
	    printf("The addr of d's container = 0x%x.\n", container_of(p, package_t, d));  
	    return 0;  
	}  


### String类的实现（常考，注意细节）

	#include<iostream>
	#include<iomanip>
	using namespace std;
	
	class String{
	    friend ostream& operator<< (ostream&,String&);//重载<<运算符
		friend istream& operator>> (istream&,String&);//重载>>运算符
	public:
	    String(const char* str=NULL);                //赋值构造兼默认构造函数(char)
	    String(const String &other);                 //赋值构造函数(String)
	    String& operator=(const String& other);       //operator=
	    String operator+(const String &other)const;  //operator+
	    bool operator==(const String&);              //operator==
	    char& operator[](unsigned int);              //operator[]
	    size_t size(){return strlen(m_data);};
	    ~String(void) {delete[] m_data;}
	private:
	    char *m_data; // 用于保存字符串
	};
	
	inline String::String(const char* str)   
	{
		if(!str)m_data=0;      //声明为inline函数，则该函数在程序中被执行时是语句直接替换，而不是被调用
		else {
			m_data=new char[strlen(str)+1];
			strcpy(m_data,str);
		}
	}
	
	inline String::String(const String &other)
	{
		if(!other.m_data)m_data=0;//在类的成员函数内可以访问同种对象的私有成员（同种类则是友元关系）
		else 
		{
			m_data=new char[strlen(other.m_data)+1];
			strcpy(m_data,other.m_data);
		}
	}
	
	inline String& String::operator=(const String& other)
	{
	    if (this!=&other)
	    {
	        delete[] m_data;
	        if(!other.m_data) m_data=0;
	        else
	        {
	            m_data = new char[strlen(other.m_data)+1];
	            strcpy(m_data,other.m_data);
	        }
	    }
	    return *this;
	}
	inline String String::operator+(const String &other)const
	{
	    String newString;
	    if(!other.m_data)
	        newString = *this;
	    else if(!m_data)
	        newString = other;
	    else
	    {
	        newString.m_data = new char[strlen(m_data)+strlen(other.m_data)+1];
	        strcpy(newString.m_data,m_data);
	        strcat(newString.m_data,other.m_data);
	    }
	    return newString;
	}
	
	inline bool String::operator==(const String &s)    
	{
	    if ( strlen(s.m_data) != strlen(m_data) )
	        return false;
	    return strcmp(m_data,s.m_data)?false:true;
	}
	
	inline char& String::operator[](unsigned int e)
	{
	    if (e>=0&&e<=strlen(m_data))
	        return m_data[e];
	}
	
	ostream& operator<<(ostream& os,String& str)
	{
	    os << str.m_data;
	    return os;
	}
	
	istream &operator>>( istream &input, String &s )
	{
	   char temp[ 255 ]; //用于存储输入流
	   input>>setw(255)>>temp;
	   s = temp; //使用赋值运算符
	   return input; //使用return可以支持连续使用>>运算符
	}
	
	int main()
	{
	    String str1="Aha!";
	    String str2="My friend";
	    String str3 = str1+str2;
	    cout<<str3<<"/n"<<str3.size()<<endl;
		return 0;
	}

### C语言内存分布图

<table border="1">
    <tr>
        <td>最低内存地址</td>
    </tr>
    <tr>
        <td>代码区(code area)</td>
    </tr>    
    <tr>
        <td>数据区(data area)：：<br>文字常量区<br>未初始化全局变量和静态变量区<br>已初始化全局变量和静态常量区</td>
    </tr>
    <tr>
        <td>堆区(heap area)</td>
    </tr>
    <tr>
        <td>栈区(stack atea)</td>
    </tr>
    <tr>
        <td>命令行参数区和环境变量</td>
    </tr>  
    <tr>
        <td>最高内存地址</td>
    </tr>

</table>

  一个由C/C++编译的程序占用的内存分为以下几个部分：
  1、程序代码区：存放函数体的二进制代码。
  2、文字常量区：常量字符串就是放在这里，程序结束后由系统释放。
  3、全局区（static）：也叫静态数据内存空间，存储全局变量和静态变量，全局变量和静态变量的存储是放一块的，初始化的全局变量和静态变量放一块区域，没有初始化的在相邻的另一块区域，程序结束后由系统释放。
  4、堆区（heap）：一般是由程序员分配释放，若程序员不释放的话，程序结束时可能由OS回收，值得注意的是它与数据结构的堆是两回事，分配方式倒是类似于数据结构的链表。
  5、栈区（stack）：又编译器自动分配释放，存放函数的参数值，局部变量的值等，其操作方式类似于数据结构的栈。

  堆和栈的区别：
  一、由以上综述就可以得知，他们程序的内存分配方式不同。
  二、申请和响应不同：
   1、申请方式：stack由系统自动分配，heap需要程序员自己申请，C中用函数malloc分配空间，用free释放，C++用new分配，用delete释放。
   2、申请后系统的响应：
  栈：只要栈的剩余空间大于所申请的空间，体统将为程序提供内存，否则将报异常提示栈溢出。
  堆：首先应该知道操作系统有一个记录内存地址的链表，当系统收到程序的申请时，会遍历该链表，寻找第一个空间大于所申请的空间的堆结点，然后将该结点从空闲结点链表中删除，并将该结点的空间分配给程序。另外，对于大多数系统，会在这块内存空间中的首地址处记录本次分配的大小，这样代码中的delete或free语句就能够正确的释放本内存空间。另外，由于找到的堆结点的大小不一定正好等于申请的大小，系统会将多余的那部分重新放入空闲链表中。
  三、 申请的大小限制不同：
   栈：在windows下，栈是向低地址扩展的数据结构，是一块连续的内存区域，栈顶的地址和栈的最大容量是系统预先规定好的，能从栈获得的空间较小。
   堆：堆是向高地址扩展的数据结构，是不连续的内存区域，这是由于系统是由链表在存储空闲内存地址，自然堆就是不连续的内存区域，且链表的遍历也是从低地址向高地址遍历，堆得大小受限于计算机系统的有效虚拟内存空间，由此空间，堆获得的空间比较灵活，也比较大。
  四、申请的效率不同：
   栈：栈由系统自动分配，速度快，但是程序员无法控制。
   堆：堆是有程序员自己分配，速度较慢，容易产生碎片，不过用起来方便。
  五、堆和栈的存储内容不同：
   栈：在函数调用时，第一个进栈的是主函数中函数调用后的下一条指令的地址，然后是函数的各个参数，在大多数的C编译器中，参数是从右往左入栈的，当本次函数调用结束后，局部变量先出栈，然后是参数，最后栈顶指针指向最开始存的地址，也就是主函数中的下一条指令。
   堆：一般是在堆得头部用一个字节存放堆得大小，具体内容由程序员安排。
