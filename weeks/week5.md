## Day 25  结构化网格和非结构化网格

> [CEM_CFD划分六面体结构网格](https://zhuanlan.zhihu.com/p/158111591))
>
>  [Fluent-ICEM六面体以及块网格划分原理及介绍](https://ishare.iask.sina.com.cn/f/258XTBhwD1R.html)
> 
> [ICEM网格划分原理](https://wenku.baidu.com/view/b6b57edfad51f01dc281f1df.html)

- [x] 结构化网格

1. 定义
结构化网格是指网格区域内所有的内部点都具有相同的毗邻单元,为六面体；在拓扑结构上矩形区域内的均匀网格，其节点定义在每一层的网格线上，且每一层上节点数都相等，但这样复杂外形的贴体网格生产比较困难。

2. 优点
在结构化网格中，每一个节点及控制容积的几何信息必须加以存储，但该节点的邻点关系则是可以依据网格编号的规律而自动得出的，因此数据结构简单，不必专门存储这类信息，这是结构化网格的一大优点；除此外，还具有的优点是：
* 网格生成的速度快；
* 网格生成的质量好；
* 对曲面或空间的拟合大多数采用参数化或样条插值的方法得到，区域光滑，与实际的模型更容易接近。它可以很容易地实现区域的边界拟合，适于流体和表面应力集中等方面的计算。

3. 缺点
* 适用的范围比较窄，只适用于形状规则的图形。
* 需要大量人工操作

4. 原理
创建反映实体特征的块，确定块上的节点分布，关联块与实体的点线面，把块的节点投影到实体上

5. 操作

* 需要新导入模型进行拓扑，也是一种“条件反射”操作；对于拓扑个人理解是将模型在两款软件中进行一次“交汇对接”；容差值最好不要修改，如果出现问题建议重新建模，修改犹如“无底洞”；ICEM中有四种颜色的线条，绿色指的是单独的一条线，没有面和它关联。黄色指的是只有一个面和这条线关联，说直白点也就是面的边界线；出现黄线和绿线多数情况是拓扑出现了问题，模型创建不理想。


- [x] 非结构化网格
1. 定义
非结构化网格是指网格区域内的内部点不具有相同的毗邻单元，可以是多种形状，四面体（也就三角的形状），六面体，棱形，也可以是六面体。与网格剖分区域内的不同内点相连的网格数目不同。


2. 优点
* 非结构画网格没有规则的拓扑结构，也没有层的概念。网格节点的分布是随意的，因此具有灵活性


3. 缺点
计算时需要较大的内存。


- [x] 两大网格划分方法
1. 预设方法自动划分（求解节点）
特点：操作简单，输出非结构网格，应付复杂模型，网格质量不能保证，大多需要网格修补

2. 基于附加块的网格划分
方法：创建反映实体特征的块，确定块上的节点分布，关联块与实体的点线面，把块的节点投影到实体上
特点：
* 大量人工操作
* 可以输出非结构化&结构化网格
* 网格质量高
* 简单模型


- [x] 网格精度 

计算精度主要在于网格的质量（正交性，长宽比），并不决定于拓扑

## Day 26 网格单元质量检查（Hypermesh）

对于2D单元，检查项主要包括：

- [x] 翘曲度（warpage）：
 用来衡量一个单元偏离平面的程度，仅适用于四边形单元，将四边形单元沿其对角线分成两个三角形，这两个三角形单元法向量之间的夹角（锐角）定义为该四边形网格的翘曲度。理想值=0度，可接受值<16度。

<img width="586" alt="image" src="https://user-images.githubusercontent.com/43568675/187349778-13eab73d-5721-408f-bcd8-bae0a811167a.png">



- [x] 长宽比（aspect）：单元最长边与该单元最短边之比。理想值=1，可接受值<5。

<img width="433" alt="image" src="https://user-images.githubusercontent.com/43568675/187349821-caf7a474-af54-4f65-91bd-a06d0cb258da.png">


- [x] 扭曲度（skew）：也称偏斜度，对于四边形单元定义为90度-两条中线夹角的最小值；三角形单元定义为90度-每个顶点与对边中点连线与两相邻边的中线夹角的最小值。理想值=0度，可接受值<60度。

<img width="259" alt="image" src="https://user-images.githubusercontent.com/43568675/187349935-2f246092-d699-40a3-91d2-3b825cbfaecc.png">


- [x] 弦差（chordal deviation）：用于检查网格边线对实际几何曲线的模拟情况，定义为单元边中点距曲面的最大距离。

- [x] 雅克比（jacobian）：评价一个单元偏离完美单元的程度。完美四边形单元为正方形，完美三角形单元为等边三角形。雅克比的取值在0到1之间，理想值=1，可接受值>0.6。

- [x] 长度（length）：三角形单元或四边形单元角点至对边的距离。最短距离称为最小长度min length。

- [x] 锥度（taper）：对于四边形单元，沿两条对角线可将其划分为四个三角形。锥度定义为：

Taper=1-(Atri/(0.5*Aquad))min。锥度理想值=0，可接受值<0.5。

- [x]  内角（angle）：扭曲度基于单元的全局形状，不考虑四边形或三角形的单个内角。内角用来检查单元单个内角的大小。四边形单元内角的理想值为90度，可接受值为[40, 135]度；三角形单元内角的理想值为60度，可接受值为[20, 120]度。

对于3D单元，增加检查项：

- [x] 四面体坍塌比（tet collapse）：

Tet collapse=h*1.24/A。 坍塌比理想值=1，可接受值>0.1，也就是说，对于一些不规则复杂模型，通常保证雅克比大于0.1即可以进行分析。

<img width="492" alt="image" src="https://user-images.githubusercontent.com/43568675/187349850-d9204522-e398-4ab8-9042-4d4b306cb26e.png">

附：另外体网格生成之后，首先共节点，然后通过tool->find face生成对应的表面网格，最后通过tool->edges检查面网格是否存在自由边和T形边，若存在T形边，删除重复的体网格。

附图：
<img width="580" alt="image" src="https://user-images.githubusercontent.com/43568675/187350011-231c7f4c-8c8e-4d54-9d49-55ba3f6dda77.png">

附图一 2D单元质量指标

<img width="571" alt="image" src="https://user-images.githubusercontent.com/43568675/187350039-553bd924-cfbb-4197-895b-4e85bf048d80.png">


附图二 单元质量检查控制参数
备注：上述总结参考GB/T 33582-2017。

## Day 27 ANSYS Multizone Meshing创建六面体网格 1
 
 > [ANSYS Multizone Meshing创建六面体网格](https://www.bilibili.com/read/cv8061531?from=search&spm_id_from=333.337.0.0)
 ANSYS Meshing是ANSYS Workbench的一个组件，集成了ICEM CFD、TGRID (Fluent Meshing)、CFX-Mesh、Gambit网格划分功能，具有较为强大的前处理网格划分能力。
- [x] 网格划分目录树如图1所示，网格划分基本流程一般需要考虑如下内容：

① 全局网格设置；

② 局部网格划分；

③ 网格划分问题排除；

④ 虚拟拓扑；

⑤ 预览或生成网格；

⑥ 检查网格质量等。

其中ANSYS Meshing网格划分方法中的多区Multizone Meshing划分方法基于ICEM CFD 六面体模块，能进行自动几何分解，相对扫掠方法不需要对元件切块，即可获得纯六面体网格（复杂结构依旧需要切块），对于一些球、圆柱、简易几何具有很好应用。

本文从多区Multizone Meshing方法出发，借助边尺寸控制Edge Sizing、映射面网格划分Mapped Face meshing、虚拟拓扑Virtual Topology以及模型切块操作等，对如何快速进行简单结构六面体网格划分进行案例说明。

在未来的文字中也会介绍如何对复杂结构基于顺序划分方法进行高度六面体划分的应用。 



## Day 28  ANSYS Multizone Meshing创建六面体网格 2

- [x] 六面体网格划分方法

1. 扫掠划分（Sweep Meshing）
2. 六面体支配（Hex Dominant）
3. 多区（Multizone Meshing） 
多区（Multizone Meshing）基于ICEM CFD 六面体模块，自动几何分解，对于采用扫掠方法必要时，需要对元件切块来得到纯六面体网格，但多区划分可立即对其网格划分（依旧推荐一定程度的切分），支持膨胀划分 
<img width="371" alt="image" src="https://user-images.githubusercontent.com/43568675/187831440-3f652ea4-bfe7-46e1-b1b0-03a6a41d370c.png">

* 映射网格方法（Mapped Mesh Type）包括如下：

1、Hexa ：默认方法，仅有六面体单元生成。

2、Hexa/prism：考虑划分质量与过渡，三角形会在源面出现，导致出现六面体与棱柱单元。

3、Prism ：仅棱柱单元产生，用于临近结构的生成网格为四面体情况。



* 面网格划分方法（Surface Mesh Method）包括如下：

1、Uniform：使用递归循环切割方法，能够创建高度一致的网格。

2、Pave：能够创建高曲率的面网格，相邻边有高的纵横比。

3、program controlled：根据网格尺寸设置与面特点综合使用上述两种方法。


- [x] Edge Sizing尺寸设置 


1、Element Size定义边平均单元边长。

2、 Number of Divisions定义边的单元分数。

3、偏斜类型【Bias Type】指定单元大小相对边的一端、两端或者边中心的渐变效果。

4、偏斜因子【Bias Factor】定义最大单元边长与最小单元边长的比值。

5、【Soft】选项的单元大小将会受到整体划分单元大小的功能，如基于相邻、曲率的网格设置，以及局部网格控制的影响。

6、【Hard】严格控制单元尺寸。 

<img width="594" alt="image" src="https://user-images.githubusercontent.com/43568675/187895669-00e2771a-d490-43e9-b2a1-9d3c5b337cce.png">

## Day 29 ansys workbench 工程材料属性定义及如何使用

- [x] engineering data 定义材料
1. 使用软件自带材料
Engineering Data sources
<img width="389" alt="image" src="https://user-images.githubusercontent.com/43568675/188062059-abac7427-b0f0-4305-804b-faa79dfc6cd2.png">

2. 自定义材料
<img width="1032" alt="image" src="https://user-images.githubusercontent.com/43568675/188062420-3ac3d469-936d-46de-8d9d-4a1876644f0c.png">

<img width="614" alt="image" src="https://user-images.githubusercontent.com/43568675/188061833-3295269f-9e18-486f-ba18-d175316618d0.png">
* 弹性模量（杨氏模量）
* 泊松比

## Day 30 DesignModeler

- [x] 建模环境与SolidWorks相似，但更为复杂，环境友好性低。

- [x] 在三维模型可创建imprint face，便于施加局部载荷； 

- [x] 模型存在实体（激活体）和冻结体freeze两种状态，导入模型时可选择更改，其中冻结体不可切除cut material，且在此状态下才可以完成切片，分为多个body。
* 1个part的多个实体body会自动发生merge。（All frozen bodies will be ignored when it comes to the Add, Cut, or Imprint Material operation of any features following the Freeze。） 

- [x]  可通过选择 Create > ==Body Operation==选定体，把Type设成Sew ， 并设定Create Solids?为Yes将面体转换成实体。

- [x] 2D分析有下述特征：
 （1）对树中的geometry条目，在其细节视图中的2d behavior域，有下述选项：平面应力（plane stress缺省的）--假设在Z方向上应力为0，但是应变不为0.这对于那种Z方向的尺寸远远小于X,Y两个方向尺寸的结构是合适的。如受到面内载荷的平板，或在压力或径向载荷下的圆盘。如果想输入这种模型的厚度，可以在==thickness==域中输入。
 
 （2）轴对称(axisymmetric)----假设一个3-D模型及其载荷可以通过围绕Y轴旋转一个2D的截面而形成。==对称轴必须和全局的Y轴保持一致==。几何体必须是在正X轴和X-Y面内。方向是：Y轴是轴向的，X轴是径向的，Z轴是环向。环向位移是0，环向应力和环向应变通常很重要。典型的例子是压力容器，直管，轴等。在形状优化分析中不能使用轴对称行为。
 
 （3）平面应变(plain strain)---假设Z方向上没有应变。这对于Z方向的尺寸远大于X,Y尺寸的结构是合适的。Z方向的应力不为0.例子如常的等截面构建如结构线性物体。平面应变行为在热分析或形状优化分析中不可用。
 
 （4）一般的平面应变(generalized plane strain)—相对于标准的平面应变问题而言，假设在Z方向上有一个有限的变形域。
 
 对于存在Z方向尺寸的物体，它提供了一个更实际的结果。基于物体（by body）这允许对geometry下单个的物体设置平面应力，平面应变或者轴对称选项。如果你选择了by body,则请选择单个的物体，然后为其设置单独的2-D选项。对于2-D分析，可以使用在3-D分析中同样的方式以施加载荷和支撑，载荷和结果都是X-Y面内而没有Z向分量。+     
 
 PS：下述载荷在2-D分析中不能使用：螺栓预紧载荷，线性压力，简单支撑，固定转动。- 包围体操作创建流体域更为便利；- 创建中面：如模型有不变截面积，可以用壳来离散该模型，从而可以节省时间与CPU资源。
 
 
## Day 31 workbench mechanical

- [x] 
1. 菜单栏
* 编辑 
* 显示 
* 单位 
* 工具
* 帮助

2. 树形窗口
3. 文字窗口
4. 图形窗口
5. 信息窗口
6. 状态栏
 
- [x] 主要功能
1. 赋予材料
2. 画网格
insert-> 各个选项
3. 施加边界条件
insert- > 各个选项

4. 求解 选择结果
5. 后处理 查看云图 图表等

