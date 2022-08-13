## Day 4 涡量
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

## Day 5 结构分析后处理

- [x] 主云图、变形云图、变形矢量、设置变形比例
* 主云图（变形前云图）
* 变形云图（变形后云图）
* 变形矢量 变形方向标注
* 设置变形比例（偏移）

 > [变形云图以及变形比例](https://zhuanlan.zhihu.com/p/504791441)

## Day 6 CFD中的NS方程

- [x] NS方程是建立在连续介质假设基础上

1. 流体微团假设：即NS方程所描绘的流体质点在空间上属于无穷小，但是实际上相对于分子而言又无穷大。
2. NS方程就是牛顿第二定律的运用，依旧是在经典力学的框架下。其核心本质就是动量守恒。但NS方程终究只是一个对流体在连续介质层面的物理近似，是一个对流体在分子动力学层面进行粗粒化（coarse-graining）的物理模型
3. NS方程作为偏微分方程又是点方程
4. 在各种极端情况下（例如无旋，无粘性等）有解析解。
5. 在各种不极端的情况下可以利用科学计算的方法得到各种精确度的结果（DNS，LES，RANS，等等

## Day 7 CFD求解器
- [x] 求解器类型
1. 压力基
2. 密度基 
3. 

- [ ] 

## Day 8
- [ ] 边界条件-远端位移和给定位移
1. remote displacement
2. displacement
3. 
- [ ] 


## Day 9
## Day 10
