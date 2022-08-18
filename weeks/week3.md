## Day 11 ICEM CFD 网格划分技术

> [ANSYS ICEM CFD 网格划分技术实例](https://www.bilibili.com/video/BV1HJ411K7yU?)

- [x] 内流道 & 外流场（基于DM）

1. 内流道抽取，Tools-> fill-> by cavity(or by caps)选择内流道所有相关面，新建几何体，获取内流道几何
2. 外流场区域划分，Tools-> Enclosure -> shape-box 输入六个方向的尺寸

## Day 12 ANSYS CFD的仿真分析步骤

> [“工作流程很重要”——说说ANSYS CFD的仿真分析步骤](https://zhuanlan.zhihu.com/p/78722352)

- [x] 提出问题

1. 明确仿真目的，忽略次要因素
2. 常见流体仿真目的分类

* 得到温度的分布、温度最值的位置等（如电子散热行业等）
* 得到力、力矩或压力系数分布等（如航空航天、汽车行业等）
* 得到多相流中某一相（或多相）的分布情况（如石油行业、化工行业等）
* 得到管路中的压降（能量损失）和流量分布情况（如流体机械行业等）
* 得到流场分布来配合其他的需求

- [x] 化简问题

1. 仿真区域选取
流体永久存在（循环）的流体区域，取其中一部分进行仿真分析

2. 边界条件给定
* 边界条件给定和选取的仿真区域息息相关，因此也是简化问题的重要步骤。
* 从本质上理解，边界（面）实际上是一种等效，仿真中用它们来替代其他的流体区域。
* 通过选取不同的入口，缩小计算区域，但是需要更加精确边界条件

![image](https://user-images.githubusercontent.com/43568675/184836659-2965ba2d-431f-41ee-9d06-58c8c0e90d4d.png)

如果选取①作为入口，那么只需要简答的输入即可，缺点是计算区域会很大
如果选取②③作为入口，那么虽然计算区域相对会缩小，但是给定的边界条件需要精确的分布，当然，这些分布在①中是可以直接计算的得到的。

3. 几何模型化简

* 考虑过于精细的几何细节（如螺栓形状、小凹槽等）会使网格量成指数增加
* 基于此，明晰哪些几何细节是对仿真有影响；没有影响的，一律简化

4. 物理模型选择

* 方程来代替实际的物理现象：如湍流模型、多相流模型、热辐射模型等
* 无论何种模型，都是抓住了主要矛盾、简化了次要矛盾才诞生

在明确的仿真目的下选择必要的物理模型也是可以简化问题的，如：

某液体的流动，只关注速度与压力的影响（不需要开启传热模型）
某颗粒流中颗粒体积分数很小，颗粒对流场影响可以忽略（不需要开启DPM与流场耦合计算，仅做流场后处理即可）
某真空环境下换热问题（不需要开启流动方程计算，仅计算能量方程和辐射输运方程即可）
……


- [x] 解决问题

![image](https://user-images.githubusercontent.com/43568675/184837703-119c6021-b416-489a-a912-138cb32fd68c.png)
1. 几何

* Design Modeler（简称DM）    传统的ANSYS Workbench几何处理软件，2015年随着ANSYS SCDM的加入，大部分功能都已经逐步的被移植到SCDM当中，地位也随之边缘化
* ANSYS SpaceClaim Direct Modeler（简称 SCDM）  基于直接建模思想的新一代3D建模和几何处理软件

共同点：

* SCDM/DM都具备建立几何模型的能力，而且可以与后续的ANSYS网格划分软件进行无错数据传递。
* SCDM/DM都具备丰富的几何接口，可以读取几乎所有主流CAD软件输出的文件格式。
* SCDM/DM都具备强大的几何修补/简化功能，能够将设计（生产）CAD模型快速转化为仿真CAD模型。
* SCDM/DM以与后续的ANSYS网格划分软件进行无错数据传递，可以确保我们的仿真在几何模型上真实可靠。


2. 网格

![image](https://user-images.githubusercontent.com/43568675/184838592-dd633aaa-1f24-4271-8949-004ee3992f44.png)

流体仿真初学者，建议使用Workbench Meshing
高级流体仿真工程师，建议使用Fluent Meshing
有六面体网格需求的工程师，建议使用ICEM CFD

3. 求解
* CFX
* Fluent
 
4. 后处理

* Fluent 软件本身就具备后处理能力，CFX是依托CFD-Post进行后处理
* Fluent 的计算结果也可以通过CFD-Post进行后处理。
* ANSYS 19.0的版本之后，新增了Ensight 后处理工具

![ANSYS CFD-Post 后处理模块](https://user-images.githubusercontent.com/43568675/184838867-c92f078b-882b-41ee-ba4c-a562abcd80f5.png)

![ANSYS Ensight 后处理工具](https://user-images.githubusercontent.com/43568675/184838874-b6c993c4-ca05-4623-9d44-1ac19f549750.png)

## Day 13 流体基础综合1
> [ANSYS FLUENT培训](https://www.bilibili.com/video/BV1Kp4y197t8)
> 
> [ANSYS Fluent19.0流体有限元分析视频教程]( https://www.bilibili.com/video/BV1Dt4y1x7Ms)

- [x] 流体分析基础

1. 流体分析概述
<img width="789" alt="image" src="https://user-images.githubusercontent.com/43568675/185322405-bbb8591e-4a2a-4f56-86c0-3640bf5b9b49.png">

2. 流体分析类型
<img width="689" alt="image" src="https://user-images.githubusercontent.com/43568675/185323254-48fb513d-e97e-4807-8a13-213556c8acb6.png">
* 压缩性
可压缩（一般气体可压缩性要比液体大得多，为可压缩流体，当体积变化运动比较小，可视为不可压缩）/不可压缩
* 粘性
理想流体（实际中不存在，某种条件下的近似模拟，一般把空气水等粘性比较小的流体视为理想）/粘性流体
* 旋转
无旋流动/有旋流动
* 流态
层流/湍流
* 时间
定常（流动物理量不随时间变化）/不定常
* 空间
一维/二维/三维
* 重力
重力流体/非重力流体（一般空气or其他气体流动，按非重力流体计算）
* 流速
亚声速（马赫数 <1）/跨声速(ji)/超声速

3. 流体仿真的优缺点
* 对不同设计不用一一制作样品进行验证，缩短开发周期和设计修改费用
* 实验测定困难时获取详细数据
* 直观显示说明流场状态
* 
* 复杂物理模型需要简化，伴随误差
* 数值计算本身包含误差 

4.流体相关物质特性
<img width="720" alt="image" src="https://user-images.githubusercontent.com/43568675/185335013-e3e82f1a-eb7d-43df-9dd4-b9c9c783f8dd.png">

* 密度
<img width="691" alt="image" src="https://user-images.githubusercontent.com/43568675/185335118-66f3c01b-265b-43be-8809-a08b9b948199.png">

* 粘性系数
<img width="716" alt="image" src="https://user-images.githubusercontent.com/43568675/185335205-386e268e-5cd0-464e-ba75-87b5a378d2f9.png">

* 比热
<img width="714" alt="image" src="https://user-images.githubusercontent.com/43568675/185335302-8fdcde50-1bf6-486d-a5d3-20a94c72f46a.png">

* 导热系数
<img width="732" alt="image" src="https://user-images.githubusercontent.com/43568675/185335419-fa258c94-e461-4b14-8600-8137bb7cd02e.png">


## Day 14 流体基础综合2

- [x] 流体流动方法

1. 速度，速率和流量
<img width="739" alt="image" src="https://user-images.githubusercontent.com/43568675/185336101-c2ab03ec-feb0-4453-8f07-46453d0c6102.png">

<img width="731" alt="image" src="https://user-images.githubusercontent.com/43568675/185336173-ad00cb27-8d5f-403e-a88e-5f00b21a815f.png">

2. 压力
<img width="713" alt="image" src="https://user-images.githubusercontent.com/43568675/185336269-6762e57d-f16d-4247-92a0-f85729320a0d.png">

3. 流线和脉线，迹线
<img width="733" alt="image" src="https://user-images.githubusercontent.com/43568675/185336351-0b60ba6c-ed60-4ad9-b592-dbb7617db666.png">

<img width="741" alt="image" src="https://user-images.githubusercontent.com/43568675/185336747-e22f926a-3595-49d0-89d7-e00c48b3c52e.png">

- [x] 流体流动性质

1. 压缩性和非压缩性
<img width="715" alt="image" src="https://user-images.githubusercontent.com/43568675/185337051-3d6e7975-9357-4f85-b707-d98fbb764122.png">

<img width="710" alt="image" src="https://user-images.githubusercontent.com/43568675/185337203-8b921223-5818-463a-9559-f9179585abb6.png">

<img width="720" alt="image" src="https://user-images.githubusercontent.com/43568675/185337334-3671c680-ec81-4781-8785-6d81b0930db4.png">


2. 定常和非定常
<img width="733" alt="image" src="https://user-images.githubusercontent.com/43568675/185337436-5f16c156-76ab-42de-980e-260092e4134e.png">

<img width="681" alt="image" src="https://user-images.githubusercontent.com/43568675/185337522-b3eceb11-c21a-4ba4-8853-3d443b5da165.png">

3. 伯努利原理
<img width="749" alt="image" src="https://user-images.githubusercontent.com/43568675/185337636-f77ab3bb-9fe3-496e-b4e5-65650585c959.png">

<img width="719" alt="image" src="https://user-images.githubusercontent.com/43568675/185337954-6f35ca06-4a75-45ee-a0e7-6f68410ac12c.png">

* 衍生 马格努斯效应

4. 层流和湍流
<img width="678" alt="image" src="https://user-images.githubusercontent.com/43568675/185338414-51567de8-c558-4de3-9d8c-0a82babd1388.png">

<img width="707" alt="image" src="https://user-images.githubusercontent.com/43568675/185338499-cd75cd91-6116-44d9-b875-1bb9bfe0c968.png">

5. 雷诺数
<img width="705" alt="image" src="https://user-images.githubusercontent.com/43568675/185338684-f97e148b-634e-4de9-b607-52e224695c99.png">

<img width="731" alt="image" src="https://user-images.githubusercontent.com/43568675/185338719-63a5842e-9d50-432f-82b4-7b2e1d362ecb.png">

<img width="747" alt="image" src="https://user-images.githubusercontent.com/43568675/185339057-f2e62585-13c9-431a-aacb-f13ec3f6605c.png">

- [x] 热的基础概念
1. 热与温度
<img width="710" alt="image" src="https://user-images.githubusercontent.com/43568675/185339322-da698c6f-0619-4f2c-a122-48502405c344.png">

<img width="729" alt="image" src="https://user-images.githubusercontent.com/43568675/185339390-b84dd967-cd72-4da1-9325-f5905136f3e9.png">

 
2. 浮力
<img width="721" alt="image" src="https://user-images.githubusercontent.com/43568675/185339658-7319f347-39a5-498e-877b-1d5af669d707.png">

4. 自然对流和强制对流
<img width="720" alt="image" src="https://user-images.githubusercontent.com/43568675/185340022-ceef0e48-3d85-482e-a60d-256d2507c9bc.png">

5. 热的传递形态
<img width="738" alt="image" src="https://user-images.githubusercontent.com/43568675/185340219-f487be3c-3e7d-48e6-a285-047c95a663d8.png">

* 热传导
<img width="739" alt="image" src="https://user-images.githubusercontent.com/43568675/185340326-12388f91-d864-4904-95f0-9d7c5247bd11.png">

* 热对流
<img width="753" alt="image" src="https://user-images.githubusercontent.com/43568675/185340618-7d7dd93d-ff59-4acc-9055-1fa7b09acbb0.png">

* 热辐射
<img width="729" alt="image" src="https://user-images.githubusercontent.com/43568675/185340697-4f7f48f1-3177-4b70-befc-7690bd5539c3.png">

<img width="732" alt="image" src="https://user-images.githubusercontent.com/43568675/185340836-8b50d184-75c7-4a84-bc89-455081f1bc76.png">
