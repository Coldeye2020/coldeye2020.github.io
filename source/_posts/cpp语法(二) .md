---
title: Cpp(二)Cpp中级语法
date: 2021-04-17 00:45:22
categories:
- Tech 
- Cpp
tags: [Cpp, STL]
mathjax: false
urlname: cpp_grammar_intermediate_2
keywords: [Cpp, STL]
description:
---

{% note info %}

**说明**

本文是在`大三期间`看`北京大学 李葛老师`的`C语言基础与进阶`网课所做笔记，后并未勘误，如有错误，请谅解
{% endnote %}

<!--more-->

## C语言基础与进阶

### 递归基础部分

#### [流感传染](http://pkuic.openjudge.cn/hw06/6/)

##### 题目描述

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20210417114448702.png)

##### 代码部分

```c++
#include <iostream>
using namespace std;


int main (){
    char area[100][100] = {'\0'};
    int n;
    cin >> n;
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= n; j++){
            cin >> area[i][j];
        }
    int m;
    cin >> m;
    for(int day = 1; day <= m; day++){
        for(int i = 1; i <= n; i++)
            for(int j = 1; j <= n; j++){
                if(area[i][j] == 'w')
                {
                    area[i][j] = '@';
                }
            }
        for(int i = 1; i <= n ; i++)
            for(int j = 1; j <= n; j++){
                if(area[i][j] == '.')
                {
                    if ((area[i-1][j] == '@') + (area[i+1][j] == '@') + (area[i][j+1] == '@') + (area[i][j-1] == '@'))
                    {
                        area[i][j] = 'w';
                    }
                    
                }
            }
    }
    int num = 0;  
    for(int i = 1; i <= n ; i++){
        for(int j = 1; j <= n; j++){
            if(area[i][j] == '@')
                num++;
        }
    }
    
    cout<<num;
}
```



#### [扩号匹配问题](http://pkuic.openjudge.cn/hw07/4/)

##### 题目描述

![image-20210417114705852](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20210417114705852.png)

##### 代码部分

```c++
#include <iostream>
using namespace std;

int flag = 0;

char *F(char *str_l){
    while(*str_l != '\0'){
        if(*str_l != '('){
            if(*str_l == ')'){
                if(flag == 0)
                {
                    *str_l = '?';
                    return F( str_l + 1);
                }
                else{
                    flag--;
                    *str_l = ' ';
                    return str_l;
                }
           }
            else{
                *str_l = ' ';
                str_l++;
            }
        }
        else{
            flag++;
            char *temp = F(str_l+1);
            if(*temp == '\0'){
                *str_l = '$';
                return temp;
            }
            else{
                *str_l = ' ';
                str_l = ++temp;
            }
                
        }
    }    
    return str_l;
}

int main(){
    char str[100];
    while(cin>>str){
        cout<<str<<endl;
        F(str);
        cout<<str<<endl;
        flag = 0;
    }
}
```





#### [八皇后问题](http://pkuic.openjudge.cn/dg4/2/)

##### 题目描述

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20210417115106202.png)

##### 代码部分

```c++
#include <iostream>
using namespace std;

int flag = 0, flag2 = 0;
int chess[10][10] = {0};

bool check(int row, int column){
    int *pointer = &chess[row][column];
    for(pointer--; *pointer != -1; pointer--)
        if(*pointer == 1){
            return false;
        }
    pointer = &chess[row][column];
    for(pointer+= 9; *pointer != -1; pointer += 9){
        if(*pointer == 1){
            return false;
        }
    }
    pointer = &chess[row][column];
    for(pointer -= 11; *pointer != -1; pointer -= 11){
        if(*pointer == 1){
            return false;
        }
    }
    return true;
}

void squeen(int num){
    if (num == 9)
    {
        flag++;
        cout<<"No. "<<flag<<endl;
        for(int i = 1; i < 9; i++){
            for(int j = 1; j < 9; j++)
                cout << chess[i][j]<<" ";
            cout<<endl;
        }
        return;
    }
    for(int i = 1; i < 9; i++){
        chess[i][num] = 1;
        if(check(i, num)){
            squeen(num+1);
        }
        chess[i][num] = 0;
    }
    return;
}

int main(){
    for(int i = 0; i < 10; i++){
        chess[0][i] = -1;
        chess[9][i] = -1;
        chess[i][0] = -1;
        chess[i][9] = -1;
    }
    squeen(1);
}
```





#### [棋盘跳马问题](http://poj.org/problem?id=2243)

##### 题目描述

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20210417115629826.png)

##### 代码部分

题目描述和代码部分并不是很一样，代码写的是具有障碍的跳马问题

还没有规范输出，但是思路基本是对的，我是选取6X6的棋盘，固定右上角为终点格子，这个也可以自己写一个checkend()函数自行检验，此时可以输入一串字符串来表示这个棋盘，`@`代表障碍格子，`.`代表正常格子，`S`代表起始格子，`E`代表终点格子，输出时`S`到`E`的最短步数

```Cpp
#include <iostream>
using namespace std;


int history[8][8] = {0}; 
char panel[8][8] = {'\0'};

struct position{
    int x;
    int y;
    position *next;
    position *ahead;
} source;


position *add_position(position *head, int x, int y){
    position *temp = head;
    while(temp->next != NULL) temp = temp->next;
    temp->x = x;
    temp->y = y;
    position *extra = new position;
    temp->next = extra;
    extra->ahead = temp;
    extra->next = NULL;
    return head;
}
 
position *getLegalMove(position *head, int x, int y){
    if(panel[x+1][y] != 'b' && panel[x+1][y] != '@'){
        if(panel[x+2][y+1] != 'b' && panel[x+2][y+1] != '@' && panel[x+2][y+1] != 'S') add_position(head, x+2, y+1);
        if(panel[x+2][y-1] != 'b' && panel[x+2][y-1] != '@' && panel[x+2][y-1] != 'S') add_position(head, x+2, y-1);
    }
    if(panel[x-1][y] != 'b' && panel[x-1][y] != '@'){
        if(panel[x-2][y+1] != 'b' && panel[x-2][y+1] != '@' && panel[x-2][y+1] != 'S') add_position(head, x-2, y+1);
        if(panel[x-2][y-1] != 'b' && panel[x-2][y-1] != '@' && panel[x-2][y-1] != 'S') add_position(head, x-2, y-1);
    }
    if(panel[x][y+1] != 'b' && panel[x][y+1] != '@'){
        if(panel[x-1][y+2] != 'b' && panel[x-1][y+2] != '@' && panel[x-1][y+2] != 'S') add_position(head, x-1, y+2);
        if(panel[x+1][y+2] != 'b' && panel[x+1][y+2] != '@' && panel[x+1][y+2] != 'S') add_position(head, x+1, y+2);
    }
    if(panel[x][y-1] != 'b' && panel[x][y-1] != '@'){
        if(panel[x-1][y-2] != 'b' && panel[x-1][y-2] != '@' && panel[x-1][y-2] != 'S') add_position(head, x-1, y-2);
        if(panel[x+1][y-2] != 'b' && panel[x+1][y-2] != '@' && panel[x+1][y-2] != 'S') add_position(head, x+1, y-2);
    }
    return head;
}

int step(position des){
    int R = 100, Q = 100;
    position *head = new position, *temp;
    position mainsource = source;
    head->next = NULL;
    head = getLegalMove(head, source.x, source.y);
    temp = head; 
    while(temp->next!=NULL){
        if(history[temp->x][temp->y] != -1){
            Q = history[temp->x][temp->y];
        }
        else{
            if (panel[temp->x][temp->y] == 'E')
            {
                return 1;
            }
            source.x = temp -> x;
            source.y = temp -> y;
            panel[temp->x][temp->y] = 'S';
            Q = step(des);
            history[temp->x][temp->y] = Q;
            source = mainsource;
            panel[temp->x][temp->y] = '.';
        }
        if(R > Q) 
            R = Q;
        temp = temp->next;
    }
    return R+1;
}

int main(){
    for (int i = 1; i < 7; i++)
    {
        for (int j = 1; j < 7; j++)
        {
            cin>>panel[i][j];
        }
    }
    
    for(int i = 0; i < 8; i++){
        for(int j = 0; j < 8; j++){
            if(panel[i][j] == 'S'){
                source.x = i;
                source.y = j;
            }
            if(i == 0 || i == 7 || j == 0 || j ==7) panel[i][j] = 'b';
            history[i][j] = -1;
        }
    }
    position e = {1, 6};
    cout << step(e);
}
```

