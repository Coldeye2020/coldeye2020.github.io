---
title: Cpp(一)Cpp中级语法
date: 2020-04-2 11:20:15
categories:
- Tech 
- Cpp
tags: [Cpp, STL]
mathjax: false
urlname: cpp_grammar_intermediate
keywords: [Cpp, STL]
description:
---

{% note info %}

**说明**

本文是在`大二期间`因疫情缘故无法返校看`北京大学 郭炜老师`的`C++进阶`网课所做笔记，后并未勘误，如有错误，请谅解
{% endnote %}

<!--more-->

##C程序进阶课程

### 递归基础部分

#### 反向输出读取的字符串（递推）

##### 运行结果

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172726.png)

##### 代码部分

```C++
#include<iostream>

using namespace std;

int recur(){
	char c;
	c=cin.get();
	if(c!='\n')
		recur();
	cout<<c;
	return 0;
}

int main(){
	recur();
	return 0;
}
```



#### 进制转换（连续动作）

##### 运行结果

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172727.png)

##### 代码部分

```c++
#include<iostream>
using namespace std;

int convert(int x){
	if((x/2)!=0){
		convert(x/2);
		cout<<x%2;
	}
	else
		cout<<x;
}

int main(){
	int x;
	cin>>x;
	convert(x);
	return 0;
}
```

#### 汉诺塔问题(连续动作)

##### 运行结果

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172728.png)

##### 代码部分

```c++
#include<iostream>
using namespace std;

void move(int i,char a,char b,char c){
	if(i==1){
		cout<<"把一个盘子从"<<a<<"移动到"<<c<<endl; 
	}
	else{
		move(i-1,a,c,b);
		cout<<"把一个盘子从"<<a<<"移动到"<<c<<endl; 
		move(i-1,b,a,c);//1.把上面的全借助C移动到B 2.最后一个移动到C 3.B上的全部借助A移动到C
	}
}

int main(){
	int n;
	cin>>n;
	move(n,'a','b','c');
	return 0;
}

```

##### **分析**

+ 理解**连续的动作**是什么是什么

+ 搞清楚**不同次动作之间的关系**是什么（f(n)与f(n-1)之间的关系）

+ 搞清楚**边界条件**是什么（初始值，初始操作）

  

#### 逆波兰表达式（自动分析过程）

##### 运行结果

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172729.png)

##### 代码部分

```c++
#include<iostream>
#include<cstdlib>
using namespace std;

double notation(){
	char str[10];
	cin>>str;//遇到" "时停止，所以分析时要跟着标识指针的位置分析
	switch(str[0]){
	case'+':return notation()+notation();//当检测到运算符的时候，自动转化成两个表达式运算
	case'-':return notation()-notation();
	case'/':return notation()/notation();
	case'*':return notation()*notation();
	default:return atof(str); //把字符串转化成函数
	}
}

int main(){
	cout<<notation()<<endl;
	return 0;
}
```

#### 分苹果（自动分析过程）

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321173034.png)

##### 运行结果![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321173034.png)

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172730.png)

##### 代码部分

```c++
#include<iostream>
using namespace std;

double count(int m,int n){
	if(n<=1||m<=1)
		return 1;
	else if(m<n)
		return count(m,m);//当苹果数小时，永远会有填不满的盘子，而这些多的盘子对结果无影响
	else	
		return count(m,n-1)+count(m-n,n);/*当苹果数大时分为两种情况:有盘子没被填满和每个盘子上都有											  至少一个苹果*/
}

int main(){
	int apple,plane;
	cin>>apple>>plane;
	cout<<count(apple,plane)<<endl;
	return 0;
}
```

##### 分析

+ 分析**函数**能够给出答案
+ 在**利用这个函数**的基础上，分析**如何解决问题**
+ 搞清楚 在**最简单的情况**下 **答案** 是什么

### 数据结构基础

#### 倒置数组（指针变量）:star:

##### 运行结果

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172731.png)

##### 代码部分

```C++
#include<iostream>
#include<iomanip>
using namespace std;

int main(){
	int a[10],*p=NULL,*q=NULL;
	for(p=a;p<a+10;p++)
		cin>>*p;
	for(p=a,q=a+9;p<q;p++,q--){
		*p^=*q;
		*q^=*p;
		*p^=*q;
	}
	for(p=a;p<a+10;p++)
		cout<<setw(3)<<*p;
	return 0;
}
```

#### 矩阵乘法（二维数组）:star::star:

```C++
#include<iostream>
#include<iomanip>
using namespace std;

int main(){
	int col1,row1,col2,row2,matrix1[100][100],matrix2[100][100],result[100][100]={0};
	cin>>row1>>col1;
	if(col1>100||col1>100){
		cout<<"too large";
		return 0;
	}
	for(int i=0;i<row1;i++){
		for(int j=0;j<col1;j++){
			cin>>matrix1[i][j];
		}	
	}
	cin>>row2>>col2;
	if(col2>100||col2>100){
		cout<<"too large";
		return 0;
	}
	else if(col1!=row2){
		cout<<"error";
		return 0;
	}
	for(int i=0;i<row2;i++){
		for(int j=0;j<col2;j++){
			cin>>matrix2[i][j];
		}	
	}
	for(int i=0;i<row1;i++){
		for(int j=0;j<col2;j++){
			for(int k=0;k<col1;k++){
				result[i][j]+=matrix1[i][k]*matrix2[k][j];
			}
		}
	}
	for(int i=0;i<row1;i++){
		for(int j=0;j<col2;j++){
				cout<<setw(4)<<result[i][j]<<" ";
		}
		cout<<endl;
	}
}
```

#### 平方根函数:star:

### 习题部分

#### 	四大湖（枚举）:star::star:

##### 	题目描述

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172733.png)

​	

##### 	运行结果

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172732.png)

##### 代码部分

```C++
#include<iostream>
#include<cstdlib>
using namespace std;

int main(){
	int a,b,c,d;//代表a、b、c、d四人说的话说对的数量
	int x,y,z,w;//代表鄱阳湖、洞庭湖、太湖、洪泽湖 的排名。1是最大，4是最小
	for(x=1;x<=4;x++){
		for(y=1;y<=4;y++){
			if(x==y)
				continue;
			else{
				for(z=1;z<=4;z++){
					if(y==z||x==z)
						continue;
					else{
						w=10-x-y-z;//可以直接有前面的x,y,z确定
						a=(y==1)+(w==4)+(x==3);//记录下说对的个数
                    	b=(w==1)+(y==4)+(x==2)+(z==3);
                  	  	c=(w==4)+(y==3);
                   		d=(x==1)+(z==4)+(w==2)+(y==3);
                        if(a*b*c*d==1){//检验是否满足每人说对一个
                        	cout<<x<<endl<<y<<endl<<z<<endl<<w<<endl;
                        	return 0;
						}						
					}
			}	
			}
		}
	} 
	cout<<"No answer";
	return 0;
}
```

#### 流感传染（模拟）​ ​ ​ ​ :star::star:

##### 题目描述

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172736.png)



##### 运行结果

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172734.png)

##### 代码部分

```c++
#include<iostream>
using namespace std;
int n,m;//设置全局变量可能会导致一些问题，不过也可以带来便利
char a[102][102]={0};//设置A组作为实际情况组
int  b[102][102]={0};//设置B组作为预感染组(即明天时可能会出现的感染情况)

void input(){
	for(int i=1;i<=n;i++){
		for(int j=1;j<=n;j++){
			cin>>a[i][j];
		}
	}
}//输入函数，将字符输入

void check(){
	for(int i=1;i<=n;i++){
		for(int j=1;j<=n;j++){
			cout<<a[i][j];
		}
		cout<<endl;
	}
}//检查函数，在程序出错时，利用输出A组和B组的形式，可以直观的的观察到A组和B组的真实情况，便于改错

int count(){
	int m=0;
	for(int i=1;i<=n;i++){
		for(int j=1;j<=n;j++){
			if(a[i][j]=='@'){
				m++;
			}
		}
	}
	cout<<m;
}//计数函数，通过判断是否A组中有多少@来进行记数

void initb(){
	for(int i=1;i<=n;i++){
		for(int j=1;j<=n;j++){
			if(a[i][j]=='@')
				b[i][j]=-1;
			else if(a[i][j]=='#')
				b[i][j]=0;
			else
				b[i][j]=1;
		}
	}
}//初始化B函数，应该是多余的


void infb(){
	for(int i=1;i<=n;i++){
		for(int j=1;j<=n;j++){
			if(a[i][j]=='@'){
				b[i-1][j]=-1;
				b[i+1][j]=-1;
				b[i][j-1]=-1;
				b[i][j+1]=-1;
			}
		}
	}
}//预感染函数，将根据A组当天情况，进行预感染判断，并将情况存储到B中

void btoa(){
	for(int i=1;i<=n;i++){
		for(int j=1;j<=n;j++){
			if(b[i][j]==-1&&a[i][j]=='.')
				a[i][j]='@';
			else if(b[i][j]==-1&&a[i][j]=='#')
				b[i][j]=0;
		}
	}
}//感染函数，将根据前天B组的预感染情况，结合A组的真实情况，进行感染判断，并储存在A中

int main(){
	cin>>n;
	input();
	initb();
	cin>>m;
	for(int i=1;i<m;i++){
		infb();
		btoa();
	}
	count();
}
```

#### 括号匹配（自动分析）:star::star::star::star:

##### 题目描述

每个')'括号都有对应的'('，反之亦然

##### 运行结果

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172735.png)



##### 代码部分

```C++
#include<iostream>
#include<cstring> 
using namespace std;
int b=0;//我们想要match函数有两个输出返回值，所以选择了定义全局变量的方式，来代表其另外一个返回值
/*我们利用递归基础中自动分析的原理，先假设了一个函数match可以检查一个'('左括号右边是否存在一个可以与之匹配的')'右括号(并且保证中间的所有嵌套括号(比初始检验第一个级别的括号)都有得匹配)，接受两个值：1.字符串 2.开始检查的标识指针位置，返回两个值：1.bool型表示匹配成功与否 2.int型表示成功匹配时的标识指针位置*/
int match(char str[],int s){
	if(strlen(str)==s){
		return (b=true,-1);//为了保证完全检验，且区别于(右括号结尾b为真)的情况，我们须将true与另一变量绑定进行标注
	}
	else{
		if(str[s]=='('){//如果侦测到一个左括号,则我们需要将其进行检验，看是否有与之匹配的右括号
			int n;
			n=match(str,s+1);//检验左括号是否能被成功匹配
			if(b==false)
				return (b=false,n);//如果返回是假，则说明匹配失败，直接返回假
			else{
             if(str[n]==')')
					return match(str,n+1);//如果返回是真，说明匹配成功了，再检验右边是否有同级的
				else
					return false；
/*值得注意的是，当最后一个多出来个左括号时，会继续调用函数，此时指针指到了外面，所以会返回第一层判断中的true和20，可能会导致一些不必要的错误，直接加一个判断条件，即如果指出去了还没有匹配成功的话就输出False，就可以使得错误被避免了*/
          }
		}
		else{/*检测到一个右括号：1.如果左边的左括号用完了，函数会直接输出假真到main中，所以我们为了和因为完全检验完			输出的真，进行区别，我们把上面一个真与另外一个变量绑定在一起 2.如果左边还有左括号，将返回1与之匹配*/
			return (b=true,s);
		}
	}
}

int main(){
	char str[20],m;
	cin>>str;
	m=match(str,0);
	if(b==true&&m==-1)//
		cout<<"valid"<<endl;
	else
		cout<<"invalid"<<endl;
}
```





























## 常用表与库函数

### 表

#### 算数运算符优先级表

| 优先级 | 运算符           | 名称或含义               | 使用形式                  | 结合方向 | 说明       |
| ------ | ---------------- | ------------------------ | ------------------------- | -------- | ---------- |
| 1      | []               | 数组下标                 | 数组名[常量表达式]        | 左到右   |            |
| ()     | 圆括号           | (表达式)  函数名(形参表) |                           |          |            |
| .      | 成员选择（对象） | 对象.成员名              |                           |          |            |
| ->     | 成员选择（指针） | 对象指针->成员名         |                           |          |            |
| 2      | -                | 负号运算符               | -表达式                   | 右到左   | 单目运算符 |
| (类型) | 强制类型转换     | (数据类型)表达式         |                           |          |            |
| ++     | 自增运算符       | ++变量名  变量名++       | 单目运算符                |          |            |
| --     | 自减运算符       | --变量名  变量名--       | 单目运算符                |          |            |
| *      | 取值运算符       | *指针变量                | 单目运算符                |          |            |
| &      | 取地址运算符     | &变量名                  | 单目运算符                |          |            |
| !      | 逻辑非运算符     | !表达式                  | 单目运算符                |          |            |
| ~      | 按位取反运算符   | ~表达式                  | 单目运算符                |          |            |
| sizeof | 长度运算符       | sizeof(表达式)           |                           |          |            |
| 3      | /                | 除                       | 表达式 / 表达式           | 左到右   | 双目运算符 |
| *      | 乘               | 表达式*表达式            | 双目运算符                |          |            |
| %      | 余数（取模）     | 整型表达式%整型表达式    | 双目运算符                |          |            |
| 4      | +                | 加                       | 表达式+表达式             | 左到右   | 双目运算符 |
| -      | 减               | 表达式-表达式            | 双目运算符                |          |            |
| 5      | <<               | 左移                     | 变量<<表达式              | 左到右   | 双目运算符 |
| >>     | 右移             | 变量>>表达式             | 双目运算符                |          |            |
| 6      | >                | 大于                     | 表达式>表达式             | 左到右   | 双目运算符 |
| >=     | 大于等于         | 表达式>=表达式           | 双目运算符                |          |            |
| <      | 小于             | 表达式<表达式            | 双目运算符                |          |            |
| <=     | 小于等于         | 表达式<=表达式           | 双目运算符                |          |            |
| 7      | ==               | 等于                     | 表达式==表达式            | 左到右   | 双目运算符 |
| !=     | 不等于           | 表达式!= 表达式          | 双目运算符                |          |            |
| 8      | &                | 按位与                   | 表达式&表达式             | 左到右   | 双目运算符 |
| 9      | ^                | 按位异或                 | 表达式^表达式             | 左到右   | 双目运算符 |
| 10     | \|               | 按位或                   | 表达式\|表达式            | 左到右   | 双目运算符 |
| 11     | &&               | 逻辑与                   | 表达式&&表达式            | 左到右   | 双目运算符 |
| 12     | \|\|             | 逻辑或                   | 表达式\|\|表达式          | 左到右   | 双目运算符 |
| 13     | ?:               | 条件运算符               | 表达式1? 表达式2: 表达式3 | 右到左   | 三目运算符 |
| 14     | =                | 赋值运算符               | 变量=表达式               | 右到左   |            |
| /=     | 除后赋值         | 变量/=表达式             |                           |          |            |
| *=     | 乘后赋值         | 变量*=表达式             |                           |          |            |
| %=     | 取模后赋值       | 变量%=表达式             |                           |          |            |
| +=     | 加后赋值         | 变量+=表达式             |                           |          |            |
| -=     | 减后赋值         | 变量-=表达式             |                           |          |            |
| <<=    | 左移后赋值       | 变量<<=表达式            |                           |          |            |
| >>=    | 右移后赋值       | 变量>>=表达式            |                           |          |            |
| &=     | 按位与后赋值     | 变量&=表达式             |                           |          |            |
| ^=     | 按位异或后赋值   | 变量^=表达式             |                           |          |            |
| \|=    | 按位或后赋值     | 变量\|=表达式            |                           |          |            |
| 15     | ,                | 逗号运算符               | 表达式,表达式,…           | 左到右   |            |

### 库函数

#### 流控制函数

##### 库和函数

```C++
库
#include <iostream>
#include <iomanip>
功能：
std::setw(n)：需要填充n个字符,默认填充的字符为' '空格
std::setfill：设置std::setw将填充什么样的字符，如:std::setfill('*')
std::setbase(n)：将输出数据转换为n进制
std::setprecision(n)：控制输出流显示浮点数的数字个数，C++默认的流输出数值有效位是6。
```

##### 运行测试

![](https://raw.githubusercontent.com/Coldeye2020/picturebed/master/20200321172737.png)

##### 代码演示

```C++
#include <iostream>
#include <iomanip>
using namespace std;

int main(){
    int a=1111,b=2222;
    float d=2.0,e=200003000;
    char c='*';
  	cout<<"setw()"<<endl<<a<<setw(5)<<a<<b<<endl;
    cout<<a<<setw(5)<<a<<setw(3)<<b<<endl<<endl;
	/*setw()只对其后面紧跟的输出产生作用，表示’a’共占n个元素，不足的用空格填充。若输入的内容超过setw()设置的长度，
	则按实际长度输出。setw()默认填充的内容为空格，可以setfill()配合使用设置其他字符填充。*/ 
	
	cout<<setfill('0')<<"setfill+setw()"<<endl<<setw(5)<<a<<endl;
	cout<<endl<<setw(6)<<b<<endl<<endl<<endl;
	//setfill()常常与配合setw()使用,且setfill()是作用于cout 
	
	
	cout<<endl<<endl<<"fixed"<<endl<<d<<endl;
	cout<<e<<endl;
	cout<<fixed<<d<<endl<<e<<endl;
	//fixed就是强制规定输出到流输出的数值有效位（默认6位） 
	cout<<endl<<d<<endl<<endl;
	//可以看到fixed的作用对象是cout，使其能够一直有效
    
	
	cout<<endl<<endl<<"setprecision"<<endl<<setprecision(5)<<d<<endl;
	cout<<d<<endl<<endl;
	//setprecision控制输出流显示浮点数的数字个数(C++默认的流输出数值有效位是6),其作用对象也是cout
	cout<<setfill('0');
}
```

#### 字符串函数

##### 库

```C++
#include <iostream>
#include <cstring>
```

##### 普通字符串函数

###### 复制

```C++
char *strcpy( char *destination, const char *source);//作用是复制整个字符数组到另一个字符数组，因此也就非常简洁，只有两个参数,读变量名就可以知道，前一个是要复制到的目标数组起始位置，后一个是被复制的源数组起始位置
char *strncpy( char *destination, const char *source, size_t num );//strncpy与strcpy很类似，只是可以指定复制多少个字符显然前两个参数的含义与strcpy相同，第三个参数num就是要复制的字符个数。
```

###### 连接

```C++
char * strcat(char *destination, const char *source );//strcat的功能是把一个字符数组连接到另一个字符数组的后面,前一个是目标数组，后一个是要添加到后面的源数组。
char * strncat(char *destination, const char *source, size_t num );//连接，也是可以指定字符个数,参数跟前面的套路是一样的，这里就不重复了
```

###### 比较

```C++
int strcmp(const char *str1, const char *str2 );//对两个字符数组我们可不能直接if (s > t)这样比较，要知道这样比较的可是两个字符数组的指针的地址。那么，我们就要用到strcmp函数
```

```c++
int stricmp(char *str1, char *str2);//以大小写不敏感方式比较两个串，方法同上
```

```C++
int stricmp(char *str1, char *str2);//只比较前n个字符，方法同上
```


$$
strcmp(st{r_1},st{r_2}) = \left\{ \begin{array}{l}
\begin{array}{*{20}{c}}
{}&{0}&{st{r_1} = st{r_2}}
\end{array}\\
\begin{array}{*{20}{c}}
{ < 0}&{st{r_1} < str{}_2}
\end{array}\\
\begin{array}{*{20}{c}}
{ > 0}&{st{r_1} > st{r_2}}
\end{array}
\end{array} \right.
$$

###### 查找

```cpp
const char *strchr ( const char *str, int character );//strchr函数可以在一个字符数组里找某个字符第一次出现的位置,显然前一个是原字符数组，后一个是要查找的字符
```

```cpp
const char *strstr( const char *str1, const char *str2 );//strstr函数可以在一个字符数组里查找另一个字符数组第一次出现的位置,其中前一个是文本串，后一个是模式串
```

```C++
char *strtok(char *s, const char *delim);//找找到被某些字符分割的子串，如:' ' , ',' , '.' , '?'一类，注意：1.若想找到全部子串需多次调用(可以定义一个指针变量接受返回值并输出)(后续调用时,记得将第一个参数设置为NULL) 2.再输入分割字符时，要输入字符串" ,.?"(已经包含了space ， 。 ？四个分割字符) 3.使用时会拆分掉原字符串
```

```C++
size_t strlen( const char *str );//strlen用于求一个字符数组的长度，注意它是从给定的起始位置开始不断往后尝试，直到遇到’\0’为止的，因此它的时间复杂度并不是常数级别的，而是取决于字符数组的长度，在字符数组没有变动的情况下请务必不要重复调用。那么参数毋庸置疑自然就是要求长度的字符数组了。
```

###### 转化

```C++
char *strupr(char *str)//将串中的小写字母转换为大写字母
```

```C++
char *strlwr(char *str);//用于将字符串中的字符转换为小写
```

```c++
long strtol(char *str, char **endptr, int base);//将串转换为长整数
```

![](https://cdn.jsdelivr.net/gh/Coldeye2020/picturebed/img/20200322150939.png)

![](https://cdn.jsdelivr.net/gh/Coldeye2020/picturebed/img/20200322151023.png)

![](https://cdn.jsdelivr.net/gh/Coldeye2020/picturebed/img/20200322151310.png)

##### 内存操作函数

```cpp
void * memset( void *ptr, int value, size_t num );//memset是一个非常好用的函数，不仅在字符串方面。它可以把连续一段区间的内存修改成同一个值，以字节为单位。而一个字符正好就是一个字节，这也就让memset可以很好的为字符串的区间修改提供服务。ptr指向要修改的内存块的起始地址，value是要修改成什么值，num是修改多少个
```

```c++
void *memcpy(void *destin, void *source, unsigned n);//函数的功能是从源内存地址的起始位置开始拷贝若干个字节到目标内存地址中，即从源source中拷贝n个字节到目标destin中
```

![](https://cdn.jsdelivr.net/gh/Coldeye2020/picturebed/img/20200322153108.png)

![](https://cdn.jsdelivr.net/gh/Coldeye2020/picturebed/img/20200322153126.png)

![](https://cdn.jsdelivr.net/gh/Coldeye2020/picturebed/img/20200322153848.png)

#### 标准库文件头函数

##### 库

```C++
#include<cstdlib>
```

常见算法函数

```C++
void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void*))//快速排序函数
```







## STL初步（Standard Template Library）

### Algorism（算法类）

#### 头文件

```C++
#include<algorism>
```

#### 排序算法

##### sort()

#### 二分查找算法

##### binary_search()

##### lower_bound()

##### upper_bound()



### Containers（容器类）

#### 头文件

```C++
#include <set>
```

