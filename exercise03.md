# 报告
## 题目：It is often the case that the frictional force on an object will increase as the object moves faster. A fortunate example of this is a parachutist; the role of the parachute is to produce a frictional force due to air drag, which is larger than would normally be the case without the parachute. The physics of air drag will be discuss in more detail in the next chapter. Here we consider a very simple example in which the frictional force depends on the velocity. Assume that the velocity of an object obeys an equation of the form where _a_ and _b_ are constants. You could think of _a_ as coming  from an applied force, such as gravity, while _b_ arises from friction. Note that the frictional force is negative(we assume that _b>0_), so that it opposes the motion, and that it increases in magnitude as the  velocity increases. Use the Euler mothod to solve(1.10) for _v_ as a function of time. A convenient choice of parameters is _a=10_ and _b=1_. You should find that _v_ approaches a constant value at long times; this is called the terminal velocity.
pesudocode  
a=10  
b=1  
initial_v=（手动输入，并且整型化）  
t=0  
delt_t=0.05  
process_v=initial_v  

创建list_v与list_t两个列表  

当t<5时，执行一下流程：  
process_v+(a-b*process_v)*delt_t  
t=t+delt_t  
在list_v与list_t加入新的数据  

手动计算出微分方程的解并且创建列表储存数据  

创建一个图画  
画出数值模拟与解析解的图像  
横坐标为（“Time（s）”）  
纵坐标为（“velocity（m/s）”）  
图像标题为（“velocity variation”）  
规定y轴范围为0~11  
显示图像  

下面为python代码
```python
import numpy as np
import matplotlib.pyplot as plt

"""初值设置"""
a = 10
b = 1
initial_v = int(input("please input the initial velovity:"))
t = 0
delt_t = 0.1
process_v = initial_v

"""设定两个列表储存数据"""
list_v=[process_v,] 
list_t=[t,]

"""进行计算，并将计算结果储存在列表中"""
while t<5:
    process_v = process_v + (a-b*process_v)*delt_t
    t=t+delt_t
    list_v.append(process_v)
    list_t.append(t)

"""解析解"""    
c=a-b*initial_v
ture_t=np.linspace(0,5,1000)
ture_v=(a-c*np.exp(-b*ture_t))/b

"""画图，将利用欧拉方法得到的结果与解析结果进行对比"""
plt.figure(figsize=(40,21))
plt.plot(list_t,list_v,label="$v(t)$",marker='.')
plt.plot(ture_t,ture_v,linewidth=2,color="grey")
plt.xlabel("Time(s)")
plt.ylabel("velocity(m/s)")
plt.title("velocity variation")
plt.ylim(0,11)
plt.legend()
plt.show()
```

下图为运行结果
![](https://github.com/LEIMIN123/computational_physics_N2015301020179/blob/master/32.png)
图中蓝色点线为数值计算的结果，灰色线为解析解的结果。
