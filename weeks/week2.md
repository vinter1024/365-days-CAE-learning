## Day 1 涡量
- [x] 涡量

1. 定义
流体速度矢量的旋度

[涡量场能够直接而简明地表现出涡的性质](https://www.zhihu.com/question/21761746/answer/19293141)
[流体力学中为什么要引入涡量](https://www.zhihu.com/question/31159018/answer/377602533)
补充：[什么是科里奥利力=科氏力（地转偏向力）](https://www.zhihu.com/question/28281378/answer/40197369)
[怎样理解流体力学中的拉格朗日描述和欧拉描述](https://www.zhihu.com/question/26129680/answer/32457812)

2. 计算方式

![image](https://user-images.githubusercontent.com/43568675/183391837-e04268d4-a60b-4dc1-845c-6d036aeaca5a.png)

3. 不同后处理可视化软件处理方式

| 后处理软件     |获取涡量处理方式         |
| -------------| ---------------------|
|Tecplot       |[·Analyze --> Calculate Variables-->Vorticity(X,y,z,Magnitude).    ·计算公式输入data->alter->specify equation](https://zhuanlan.zhihu.com/p/268806085) |
|Paraview      |偏微分工具：compute derivative->Vorticity|
|CFD-POST      |[新建计算公式](https://zhuanlan.zhihu.com/p/309396896)|


4. 涡识别的准则

> [常用涡识别方法的Tecplot实现](https://blog.csdn.net/weixin_42943114/article/details/114285258)
  * Q准则
  * λ2准则
  * delta准则
  * Omega准则
 
- [x] Tecplot CFD 后处理

> [tecplot流场后处理——云图、流线、涡识别处理](https://www.bilibili.com/video/BV1PG4y1q7RS)


