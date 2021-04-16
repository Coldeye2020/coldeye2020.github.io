---

title: Cpp项目(一)寻迹小车PID设计
date: 2021-04-14 15:08:22
categories:
- Tech 
- Cpp
- Pid
tags: [Cpp, PID, car]
mathjax: true
urlname: smart_car
keywords: [Cpp, PID, car design]
description:
---

{% note info %}

**说明**

本文记录了我在完成`大三下学期`的寻迹小车小组项目时的所负责的控制部分内容。
{% endnote %}

<!--more-->

{% note success %}

单片机型号：[NUCLEO-L432KC](https://os.mbed.com/platforms/ST-Nucleo-L432KC/l)

编译平台：[Mbed Online Compiler](https://ide.mbed.com/compiler/)

Mbed OS：[Mbed OS 2](https://os.mbed.com/handbook)
{% endnote %}



## 闭环控速部分（一阶PID）

### 单片机引脚图

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/nucleo_l432kc_2017_10_09.png)

### 小车车架模型

我们采用的车架结构是`ZK-4WD`，具体清单如下：

+ 小车底盘（亚克力材质） 2只

+ 直流减速电机（过EMC检测） 4只

+ 黄色轮子 4只

+ 20线测速码盘 4只

+ 紧固件 8只

+ 螺丝螺帽铜柱 若干

小车模型如下:

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/TB2H2C7ipXXXXXjXpXXXXXXXXXX_!!361121710.jpg)

### 一阶PID整体框架：

#### 速度闭环控制系统结构图

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/绘图1.svg)

#### Part1(Wheel & Speed Encoder Disk)

这部分包含车轮以及与车轮配套的测速码盘，一圈总计`20线`。

##### Function

+ 驱动小车前进
+ 产生能让测速传感器读取的信号

##### Input

+ 直流电机输出的机械能

##### Output

+ 小车的位移，速度（by Wheel）
+ 测速传感器的触发信号（by Speed Encoder Disk）

#### Part2(Sensor)

这部分我们采用的测速传感器型号为：，   时高电平，    时低电平

##### Function

+ 将光信号转换为电信号，并触发Mbed的中断以记录速度信息。

##### Input

+ 测速码盘产生的交替隔断信号

##### Output

+ Mbed的触发中断信号（by Sensor）
+ Mbed寄存器中特定值`counter`的增加（by Interrupt System in Mbed）

#### Part3(PID control)

这部分我们采用PID控制算法来实现小车各车轮速度的闭环控制。

##### Function

+ 将寄存器中的特定值`counter`换算为实际的速度值(单位 $lines/s$)

  
  $$
  speed = \frac{\Delta counter}{\Delta time}
  $$
  
+ 通过各车轮对应的counter换算得到的实际速度值来调节各Pwm口的输出，从而使实际速度趋近于设定的目标速度。

##### Input

+ `counter`值（from Registers in Mbed）
+ `counter`转换出来的实际速度值（from Counter-Speed Converter）

##### Output

+ 实际速度值（by Counter-Speed Converter）
+ PwmOut的更新值（by PID algorithm）

##### Trigger

+ 方式一：时间增量触发：距离上一次迭代时间的增量到达某一指定值时，触发PID迭代，实现速度更新。
+ 方式二：`counter`增量触发：`counter`的增量达到某一指定值时，触发PID迭代，实现速度更新。

#### Part4(PwmOut)

这部分我们采用Mbed的Pwm模块来控制直流电机的输出

##### Function

+ 控制直流电机

##### Input

+ PID的输出值（from PID algorithm）

##### Output

+ 电机的Pwm电信号

#### Part5(BDC)

这部分我们才用的是直流减速电机

##### Function

+ 提供机械能给车轮

##### Input

+ Pwm的电信号

##### Output

+ 车轮的机械能

### PID 设计：

#### PID原理

##### Wikipedia

The PID control scheme is named after its three correcting terms, whose sum constitutes the manipulated variable (MV). The proportional, integral, and derivative terms are summed to calculate the output of the PID controller. Defining ${u(t)}$ the controller output, the final form of the PID algorithm is
$$
u(t)={MV}(t)=K_{\text{p}}e(t)+K_{\text{i}}\int _{0}^{t}e(\tau )\,d\tau +K_{\text{d}}{\frac {de(t)}{dt}}
$$
where

${\displaystyle K_{\text{p}}}$is the proportional gain, a tuning parameter

${\displaystyle K_{\text{i}}}$is the integral gain, a tuning parameter

${\displaystyle K_{\text{d}}}$is the derivative gain, a tuning parameter

${\displaystyle e(t)=\mathrm {SP} -\mathrm {PV} (t)}$ is the error (SP is the setpoint, and PV(*t*) is the process variable)

$t$ is the time or instantaneous time (the present)

$\tau $ is the variable of integration (takes on values from time 0 to the present ${\displaystyle t}$

Equivalently, the [transfer function](https://en.wikipedia.org/wiki/Transfer_function) in the [Laplace domain](https://en.wikipedia.org/wiki/Laplace_transform) of the PID controller is
$$
\displaystyle L(s)=K_{\text{p}}+K_{\text{i}}/s+K_{\text{d}}s
$$
where ${\displaystyle s}$ is the complex frequency.

##### Bilibili

<iframe src="//player.bilibili.com/player.html?aid=627065033&bvid=BV1et4y1i7Gm&cid=235144459&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

#### PID更新方案(触发条件)

##### 方式一：时间增量触发

~~原理：距离上一次迭代时间的增量到达某一指定值时，触发PID迭代，实现速度更新。~~（已舍弃）

实现：

+ 通过`flipper`创建一个定时任务，规定每0.2s执行一次迭代
+ 计算当前实际速度$actual\ speed = \frac{\Delta counter}{time}$
+ 执行PID算法，`time_delta`恒定为0.2s
+ 将`counter`清零，进入下一个定时循环

问题&改进：

1. 测得速度与实际速度有误差，且该误差与小车速度以及迭代的间隔时间相关：
   + 测试结果：在我们首先对一个车轮进行PID测试，发现存在返回的速度值波动较大，于是我们将Full Pwm加在电机上，我们发现在`time_delta`为0.2s的空转测试中，返回的测得速度在95~105之间波动，明显存在一定的问题

   + 分析：我们猜测定时触发更新迭代会导致测得速度与实际速度之间存在随机的偏差，这是由于`counter`变量所表示出来的位移信息并不精确，举个具体一点例子吧！比如，实际位移应该是1.1个counter，1.5个counter和1.9个counter，这些统统都会被认为是1个counter。当然如果我们每次更新时counter的增量都很大的话，这种1以内的误差其实就并不会影响多少了。

   + 理论分析：

     + 我们假设起始点为A，我们发现当counter的增量为n时，其位移最少为n，最大为n+1，假设起始点为A'，counter增量为n时，其位移最少为n-1，最大为n。所以对于counter读数为n而言，其最小可能位移为n-1，最大可能位移为n+1![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/geogebra-export (1).svg)

     + 误差计算

       我们假设能满足合理性$\Delta time_{max} = 0.2s$，此时我们假设速度为$\omega(unit:line/s)$
       $$
       counter = \omega \times \Delta time_{max} = 0.2\omega \\
       counter_{error} = 2 \\
       error = \frac{couter_{error}}{counter}=\frac{10}{\omega} \times 100\% \\
       $$
       我们的最大速度$\omega_{max}≈100$，所以最小误差为$error_{min}≈10\%$，最小平均误差为$ave\_error_{min}=\frac{1}{2} \times error_{min}≈5\%$

       当我们速度为$\omega=50$，误差为$error≈20\%$

       显然这是不可能容忍的，除非我们将$\Delta time$设置为2s以上或者更高才能基本上满足我们的要求。

结果：

+ 由于误差过大，我们基本上排除了了这个方法
+ 但是如果后续需要添加根据长时间更新PID的策略时，我们也可以调用这个方法，尽量让$\Delta time$大于2s就可以满足我们的需要了



##### 方式二：`counter`增量触发

`counter`的增量达到某一指定值时，触发PID迭代，实现速度更新。

实现：

+ 通过`timer`创建一个计时器，用于记录连续两次PID更新之间的间隔时间$\Delta time$。
+ 在`main()`函数的循环过程中加入判断语句，规定`counter`变量的值达到10后执行一次迭代
+ 计算当前实际速度$actual\ speed = \frac{counter}{\Delta time}$ 
+ 执行PID算法，`time_delta`更新为$\Delta time$
+ 将`counter`清零，将`timer`清零，进入下一个定时循环

问题&改进：

1. 首先是停止后无法自动起步的问题

   + 测试结果：我们首先对一个车轮进行PID测试，发现小车并不能自动起步，需要手动给予一定速度后才能开始稳定运行
   + 分析：由于这种更新触发策略需要小车开始运行后才能开始持续不断的更新速度，所以小车一旦因为任何原因停下以后将不能进行下一次的速度更新，导致永远无法自动起步
   + 改进：我们可以利用PID中设定的计时器`timer`，因为每次执行PID算法时候，都会进行清零操作，所以我们很容易联想到的方法就是设定当计时器`timer`读数大于某个特定值时，将会强制执行PID算法
   + 方案改进：

2. 然后就是停止过长时间再次更新时会导致PID算法中积分项过大的问题

   然后就是起步时速度猛增的问题

   + 测试结果：我们首先对一个车轮进行PID测试，发现小车往往能够弹射起步，并维持一段时间告诉运行后之后才恢复到目标速度

   + 测试结果：在我们首先对一个车轮进行PID测试时，发现小车往往能够弹射起步，并维持一段时间告诉运行后之后才恢复到目标速度
   + 分析：`timer`的累积可能会导致PID算法中积分项过大
   + 改进：在PID更新过程中，当检测到`timer`的读数过大时，自动识别为停止起步模式，返回测得速度为0，并将$\Delta time$ 设置为0.01s

结果：

+ 我们决定采用方案二作为我们的PID更新方式

#### PID代码

##### 项目目录

```shell
└─little_car
    ├─main.cpp
    ├─pid.h
    └─mbed
        └─...
```



>当算法译平台默认支持的语言是C和C++，因为除了大一的时候学过一学期C语言，之后都没怎么学过了，所以代码写的很糙，如果要直接使用的话，请仔细检查。
>
>考虑到之后在PID Calibration过程，可能要使用到的字符串的处理，以及我之前在学习Java和Python时对类有一定的了解，所以果断采用C++。
>
>该代码是最初始版本，包含了调试时所需要的串口通信和字符串处理的代码

```c pid.h Used to define two Structures pidCalibrationand pidState
// protection against multiple includes
#ifndef SAXBOPHONE_PID_H
#define SAXBOPHONE_PID_H

#ifdef __cplusplus
extern "C"{
#endif
    typedef struct pid_calibration {
        /*
         * struct PID_Calibration
         * 
         * Struct storing calibrated PID constants for a PID Controller
         * These are used for tuning the algorithm and the values they take are
         * dependent upon the application - (in other words, YMMV...)
         */
        double kp; // Proportional gain
        double ki; // Integral gain
        double kd; // Derivative gain
    } PID_Calibration;


    typedef struct pid_state {
        /*
         * struct PID_State
         * 
         * Struct storing the current state of a PID Controller.
         * This is used as the input value to the PID algorithm function, which also
         * returns a PID_State struct reflecting the adjustments suggested by the algorithm.
         * 
         * NOTE: The output field in this struct is set by the PID algorithm function, and
         * is ignored in the actual calculations.
         */
        double actual; // The actual reading as measured
        double target; // The desired reading
        double time_delta; // Time since last sample/calculation - should be set when updating state
        // The previously calculated error between actual and target (zero initially)
        double previous_error;
        double integral; // Sum of integral error over time
        double output; // the modified output value calculated by the algorithm, to compensate for error
    } PID_State;

#ifdef __cplusplus
} // extern "C"
#endif

// end of header
#endif
```



```cpp main.cpp
#include "mbed.h"
#include "pid.h"
#include <iostream>
#include <string>
using namespace std;

Serial pc(PA_9, PA_10);

PwmOut mot1(D5); //D2配对左下轮
PwmOut mot2(D6); //D3配对左上轮
PwmOut mot3(D9); //D11配对右上轮
PwmOut mot4(D10); //A2配对右下轮

Ticker flipper;

int iterationCounter=10;
int flag=1;

class PidFirst {
    public:
        PidFirst(PinName pwm_name, PinName sensorPort, double tar=60.0): pwm(pwm_name), _interruptin(sensorPort){
            _counter = 0;
            pwm.period_ms(20);
            pwm=1;
            target = tar;
            PID_Calibration pidCali = {0.001, 0.006, 0};
            PID_State pidState = {0,target,0.2,target,0,0.1};
            _pidCalibration = pidCali;
            _pidState = pidState;
            time.start();
            _interruptin.rise(this, &PidFirst::counterFunc);
        }
        
        // Function: set target velocity
        void setTarget(double tar){
            _pidState.target = tar;
        }
        
        // Function: set pid calibration
        void setPid(double kp, double ki, double kd){
            _pidCalibration.kp = kp;
            _pidCalibration.ki = ki;
            _pidCalibration.kd = kd;
        }
        
        void counterFunc(){
            _counter++;
        }

        void counterClear(){
            _counter = 0;
        }

        int counterCheck(){
            return _counter;
        }

        // Function: return a speed and justify whether there is an error
        // Attention: if the velocity lesson than 0.25round/s there will be a bug
        double speedFunc(){
            duration = time.read_ms() / 1000.0;
            if(duration > 0 && duration < 3){
                _pidState.time_delta =  duration;
                return  _counter / duration;               
            }
            else{
                duration = 0.1;
                 _pidState.time_delta =  duration;
                return 0;
            }
            
        }

        // Function: to update the pid control factor
        void pid_iterate(){
            // 计算目标值与反馈值之间的误差
            double error = _pidState.target - _pidState.actual;
            // 计算Iterm
            _pidState.integral += (error * _pidState.time_delta);
            // 计算Pterm
            double derivative = (error - _pidState.previous_error) / _pidState.time_delta;
            // 计算pid next state
            _pidState.output = (
                (_pidCalibration.kp * error) + (_pidCalibration.ki * _pidState.integral) + (_pidCalibration.kd * derivative)
            );
            // 更新上一次的误差值为本次的误差值
            _pidState.previous_error = error;
            // 返回这次的状态
        }

        // Function: renew pid state;
        void renewPidState(){
            _pidState.actual = speedFunc();
            pid_iterate();
        }

        // Function: renew the hole motor parameter according to pid algorithm
        void renew(){
            renewPidState();
            pwm = _pidState.output;
            time.reset();
            counterClear();
        }
        
        double checkSpeed(){
            return _pidState.actual;
        }
        
        double timeCheck(){
            return time.read_ms() / 1000.0;
        }
        
        
    private:
        PID_Calibration _pidCalibration;       
        PID_State _pidState;
        double target;
        volatile int _counter;
        PwmOut pwm;
        InterruptIn _interruptin;
        Timer time;
        double duration;
};

PidFirst mot1_pid(D5, D2); 
PidFirst mot2_pid(D6, D3);
PidFirst mot3_pid(D9, D11);
PidFirst mot4_pid(D10, A2);


bool renew_motor(char _read[]){
    char *token;
    token = strtok(_read, " ");
    string flag =  token;

    token = strtok(NULL, " ");
    double kp = atof(token);

    token = strtok(NULL, " ");
    double ki = atof(token);

    token = strtok(NULL, " ");
    double kd = atof(token);

    token = strtok(NULL, " ");
    double tar = atof(token);
    
    if (flag == "S" || flag == "s")
    {
        mot1_pid.setPid(kp, ki, kd);
        mot1_pid.setTarget(tar);
        mot2_pid.setPid(kp, ki, kd);
        mot2_pid.setTarget(tar);
        mot3_pid.setPid(kp, ki, kd);
        mot3_pid.setTarget(tar);
        mot4_pid.setPid(kp, ki, kd);
        mot4_pid.setTarget(tar);
        return true;
    }
    else if(flag == "S1" || flag == "s1")
    {
        mot1_pid.setPid(kp, ki, kd);
        return true;
    }
    else if(flag == "S2" || flag == "s2")
    {
        mot2_pid.setPid(kp, ki, kd);
        return true;
    }
    else if(flag == "S3" || flag == "s3")
    {
        mot3_pid.setPid(kp, ki, kd);
        return true;
    }
    else if(flag == "S4" || flag == "s4")
    {
        mot4_pid.setPid(kp, ki, kd);
        return true;
    }
    else return false;
}

void flag_change(){
    flag = 1;
}


int main()
{
    string str = "";
    char ch;
    flipper.attach(&flag_change, 1);
    while(1){
        if(mot1_pid.counterCheck() >= iterationCounter || mot1_pid.timeCheck() >= 3){
            mot1_pid.renew();
        }
        if(mot2_pid.counterCheck() >= iterationCounter || mot2_pid.timeCheck() >= 3){
            mot2_pid.renew();
        }
        if(mot3_pid.counterCheck() >= iterationCounter || mot3_pid.timeCheck() >= 3){
            mot3_pid.renew();
        }
        if(mot4_pid.counterCheck() >= iterationCounter || mot4_pid.timeCheck() >= 3){
            mot4_pid.renew();
        }
        if(flag == 1){
            pc.printf("%f  %f  %f %f\n", mot1_pid.checkSpeed(), mot2_pid.checkSpeed(), mot3_pid.checkSpeed(), mot4_pid.checkSpeed());
            flag = 0; 
        }
        if(pc.readable()){
            ch = pc.getc();
            if(ch == 'E' || ch == 'e'){
                char chTemp[100];
                strcpy(chTemp, str.c_str());
                if(renew_motor(chTemp)){
                    pc.printf("successful!successful!successful!successful!successful!successful!successful!\n");
                }
                else{
                    pc.printf("failed!failed!failed!failed!failed!failed!failed!failed!failed!failed!\n");
                } 
                str = "";
            }
            else{
                str += ch;
            }
        }
    }
}
```



#### PID调试

（未完待续）

