## Day 46 ABAQUS 的文件系统

ABAQUS 除了数据库文件外，还包括用于输入、输出的文本文件，日志文件，信息文件，状态文件，及用于重启和结果转换或的文件等；另外，有些文件是在运行时产生，运行后自动删除。具体介绍如下（其中 model_database_name 表示模型数据库名，job_name 表示建立的工作名）：

（1）CAE 文件（model_database_name.cae）：模型数据库文件，在 ABAQUS/CAE 中直接打开，包含模型的几何、网格、载荷等各种信息及分析任务等。

（2）ODB 文件（job_name.odb）：输出数据库文件，即结果文件，可以在 ABAQUS/CAE 中直接打开，也可以输入到 cae 文件中作为 Part（部件）或 Model（模型），包含在 Step 功能模块中定义的场变量和历史变量输出结果，由 Visualization 功能模块打开。

（3）INP 文件（job_name.inp）：输入文件，属于文本文件。INP 文件可以在 Job 功能模块中提交任务时或单击 Job Manager 对话框中的【Write Input】在工作目录中生成，也可以通过其他有限元前处理软件生成，通过编辑 INP 文件可以实现一些 ABAQUS/CAE 所不支持的功能。INP 文件可以输入到 ABAQUS/CAE 中作为 Model（模型），也可以由 ABAQUS Command 直接运行。INP 文件中只包含模型的节点、单元、集合、截面和材料属性、载荷和边界条件、分析步及输出设置等信息，没有模型的几何信息，故输入的模型也是有限元模型而无实体模型。本书第二部分会对每个实例的 INP 文件进行详细的说明。

（4）PES 文件（job_name.pes）：参数更改后重写的 INP 文件。

（5）PAR 文件（job_name.par）：参数更改后重写的以参数形式表示的 INP 文件。

（6）LOG 文件（job_name.log）：日志文件，属于文本文件，包含运行 ABAQUS 的起止时间等信息。

（7）DAT 文件（job_name.dat）：数据文件，属于文本文件，记录数据和参数检查、单元质量检查、内存和磁盘估计和分析时间等信息，预处理 INP 文件时产生的错误和警告信息也会写入 dat 文件。另外，dat 文件中输出用户定义的 ABAQUS/Standard 的结果数据，ABAQUS/Explicit 的结果数据不会写入该文件。

（8）MSG 文件（job_name.msg）：信息文件，属于文本文件，详细记录计算过程中的平衡迭代次数、参数设置、计算时间及错误和警告信息等。

（9）IPM 文件（job_name.ipm）：内部过程信息文件，启动 ABAQUS/CAE 分析时开始写入，记录了从 ABAQUS/Standard 或 ABAQUS/Explicit 到 ABAQUS/CAE 的过程日志。

（10）JNL 文件（model_database_name.jnl）：文本文件，包含用于复制已存储的模型数据库的 ABAQUS/CAE 命令。

（11）STA 文件（job_name.sta）：状态文件，属于文本文件，包含分析过程信息。

（12）RPY 文件（ABAQUS.rpy）：记录运行一次 ABAQUS/CAE 所运用的所有命令。

（13）REC 文件（model_database_name.rec）：包含用于恢复内存中模型数据库的 ABAQUS/CAE 命令。

（14）PSR 文件（job_name.psr）：文本文件，参数化分析要求的输出结果。

（15）FIL 文件（job_name.fil）：结果文件，可被其他软件读入的结果数据格式。记录 ABAQUS/Standard 的分析结果，ABAQUS/Explicit 的分析结果要写入 fil 文件中则需要转换。

（16）RES 文件（job_name.res）：重启动文件，用 STEP 功能模块进行定义。

（17）MDL 文件（job_name.mdl）：模型文件，在 ABAQUS/Standard 和 ABAQUS/Explicit 中运行数据检查后产生的文件，重启动分析时需要该文件。

（18）PRT 文件（job_name.prt）：部件信息文件，包含模型的部件与装配信息，重启动分析时需要该文件。

（19）STT 文件（job_name.stt）：状态外文件，运行数据检查时产生的文件，重启动分析时需要该文件。

（20）ABQ 文件（job_name.abq）：状态文件，仅用于 ABAQUS/Explicit，记录分析、继续和恢复命令，重启动分析时需要该文件。

（21）SEL 文件（job_name.sel）：结果选择文件，仅用于 ABAQUS/Explicit，重启动分析时需要该文件。

（22）PAC 文件（job_name.pac）：打包文件，包含模型信息，仅用于 ABAQUS/Explicit，重启动分析时需要该文件。

（23）PSF（job_name.psf）：脚本文件，用户定义 parametric study（参数研究）时需要创建的文件。

（24）ODS 文件（job_name.ods）：记录场输出变量的临时运算结果，运行后自动删除。

（25）LCK 文件（job_name.lck）：用于阻止并发写入输出数据库，关闭输出数据库则自动删除。

## Day 47 Ansys 网格质量

- [x] 网格质量度量
1. 质量选项
* 单元质量
* 纵横比
* 雅克比
* 扭曲因子
* 平行误差
* 最大拐角
* 偏斜度
* 直角质量
* 可接受比
* 最差网格单元显示

2. 不同求解器对网格质量考虑
（1）fluent求解器的网格质量考虑
        * FLUENT 需要高质量的网格来避免数值发散
        * 偏斜度Skewness 主要度量
            不推荐 Skewness 过高，一般保持体网格的最大 Skewness 值 ＜0.95
            这个值和物理分析类型与单元位置紧密相关。如果网格中包含退化单元，则 FLUENT 会报告负体积，从而影响正常计算。
            0～0.25 为优秀网格，0.25～0.50 为很好的网格，0.50～0.80 为好的网格，0.80～0.95 为可以接受的网格，0.95～0.98 为坏的网格，0.98～1.00 为不能接受的网格。但在少数情况下，基于压力基求解器的 FLUENT 使用的网格可包含少量 Skewness 为 0.98 的网格单元。
        * 同时纵横比（Aspect Ratio）
        * 单元尺寸变化（Cell Size Change）。
    （2）cfx求解器的网格质量考虑
        * CFX 求解出现离散误差的来源
            流量逼近法中非正交性引入的误差
            存储和源逼近法中大网格扩展引入的误差
        * 网格正交性
            正交性度量考查的是 ip-face 面法向向量 n 与 node-to-node 节点向量 s 两者间的正交性。它们的正交性因子 =n·s，若数值大于 1/3 则符合期望。正交角 =90°-arccos（n×s），若数值大于 20°，则为可用的网格。这不同于 CFD 后处理中 Max/Min 面角，对应于边之间的面角，如果一单元在两个方向倾斜，可有一个可接受面角和一不可接受的正交角。
        * 扩展因子
            网格扩展因子度量体现了控制体质心的节点位置变化幅度。扩展因子约等于节点周围的最大单元体积和最小单元体积的比，其值小于 20 时为满足要求的网格。在 CFD 后处理中，网格扩展因子本质上和单元体积比是同样的。
        * 纵横比
            纵横比度量了控制体的伸长程度，即为节点周围每个单元最大和最小面积比的最大值，其值在 100 以下为理想值。在 CFD 后处理中，纵横比和边长度比很相似。
网格质量影响因素
    
    3. CAD引入的模型
        小边
        尖锐边和面
        面间的小缝隙或通道
        未连接的几何体
    网格分解和分布
    划分方式
    膨胀选择

- [x] 改进网格质量的方法
    1. 一般建议
        网格质量不佳
            (1) FLUENT 网格偏斜度非常高（＞0.98）。
            (2) 存在退化单元（偏斜度接近 1）。
            (3) 纵横比过高。
            (4) 存在负体积。
        改进方式
            (1) 移动网格节点。
            (2) 修整几何问题，如尖角、小边，合并面或分解几何体等。
            (3) 在 DM 中利用 Clean-up 工具简化几何体。
            (4) 调整 Meshing 的划分方法、方式、网格尺寸参数等。
            (5) 虚拟拓扑以简化几何体。
            (6) 收缩控制消除小特征。
    2. CAD问题清除
    3. 虚拟拓扑
    4. 收缩控制
    5. 网格尺寸和膨胀设置

## Day 48 ABAQUS 分析模块

ABAQUS 包括三个主要的分析模块：ABAQUS/Standard、ABAQUS/Explicit 和 ABAQUS/CFD。此外，ABAQUS/Standard 中还附带了 ABAQUS/Aqua、ABAQUS/Design 及 ABAQUS/Foundation 三个特殊用途的分析模块。另外，ABAQUS 还提供了 MOLDFLOW 接口和 ADAMS 接口。

ABAQUS/CAE 的集成工作环境，包括了 ABAQUS 的模型建立、交互式提交作业、监控运算过程及结果评估等能力，如图所示。
特殊需求的用户可参阅《ABAQUS/CAE User's Manual》等帮助文档。


<img width="442" alt="image" src="https://user-images.githubusercontent.com/43568675/191414309-1b676802-0159-4e05-8045-b0e753059e05.png">

- [x] ABAQUS/Standard

ABAQUS/Standard 是一个通用的分析模块。它能够求解广泛领域的线性和非线性问题，包括静态分析、动力分析、结构的热响应的分析，以及其他复杂非线性耦合物理场的分析。

ABAQUS/Standard 为用户提供了动态载荷平衡的并行稀疏矩阵求解器、基于域分解并行迭代求解器和并行的 Lanczos 特征值求解器，可以对包含各种大规模计算的问题进行非常可靠的求解，并进行一般过程分析和线性摄动过程分析。

- [x] ABAQUS/CAE

ABAQUS/CAE（Complete ABAQUS Environment）是 ABAQUS 的交互式图形环境。它可以便捷地生成或者输入分析模型的几何形状，为部件定义材料特性、边界条件、载荷等模型参数。

ABAQUS/CAE 具有强大的几何体划分网格的功能，可以检测所形成的分析模型，并在模型生成后提交、监视和控制分析作业，最后通过 Visualization 可视化模块显示得到的结果。

ABAQUS/CAE 是目前为止唯一采用「特征」（feature-based）参数化建模方法的有限元前处理程序。用户可通过拉伸、旋转、放样等方法来创建参数化几何体，也可以导入各种通用 CAD 系统建立的几何体，并运用参数化建模方法对模型进行编辑。

在 ABAQUS/CAE 中，用户能够方便地根据个人的需求设置 ABAQUS/Standard 或 ABAQUS/Explicit 对应的材料模型和单元类型，并进行网格划分。对部件间的接触、耦合、绑定等相互作用，ABAQUS 也能够方便地定义。

- [x] ABAQUS/Explicit

ABAQUS/Explicit 为显式分析求解器，适用于模拟短暂、瞬时的动态事件，以及求解冲击和其他高度不连续问题；此外，它对处理改变接触条件的高度非线性问题也非常有效，能够自动找出模型中各部件之间的接触对，高效地模拟部件之间的复杂接触，如模拟成型问题。它的求解方法是在短时间域内以很小的时间增量步向前推出结果，而无须在每个增量步求解耦合的方程系统和生成总刚。

ABAQUS/Explicit 拥有广泛的单元类型和材料模型，但是它的单元库是 ABAQUS/Standard 单元库的子集。它提供的基于域分解的并行计算仅可进行一般过程分析。此外，需要注意的是，ABAQUS/Explicit 不但支持应力/位移分析，而且支持耦合的瞬态温度/位移分析、声—固耦合的分析。

可见，ABAQUS/Explicit 和 ABAQUS/Standard 具有各自的适用范围，它们互相配合使得 ABAQUS 功能更加灵活和强大。有些工程问题需要二者的结合使用，以一种求解器开始分析，分析结束后将结果作为初始条件交与另一种求解器继续进行分析，从而结合显式和隐式求解技术的优点。

- [x] ABAQUS/CFD

ABAQUS/CFD 是 ABAQUS 新增加的流体仿真模块，新模块的增加使得 ABAQUS 能够模拟层流、湍流等流体问题，以及热传导、自然对流问题等流体传热问题。该模块的增加使得流体材料特性、流体边界、载荷，以及流体网格等与流体相关的前处理定义等都可以在 ABAQUS/CAE 里完成，同时还可以用 ABAQUS 输出等值面、流速矢量图等多种流体相关后处理结果。ABAQUS/CFD 使得 ABAQUS 在处理流—固耦合问题时拥有更优秀的表现，配合使用 ABAQUS/Explicit 和 ABAQUS/Standard，使得 ABAQUS 更加灵活和强大。

- [x] ABAQUS/View

ABAQUS/View 是 ABAQUS/CAE 的子模块，后处理功能中的可视化模块（Visualzation）就包含其中。

- [x] ABAQUS/Design

ABAQUS/Design 扩展了 ABAQUS 设计敏感度分析（DSA）中的应用。设计敏感度分析可用于预测设计参数变化对结构响应的影响。它是一套可选择模块，可以附加到 ABAQUS/Standard 模块。本书将不介绍该模块。

- [x] ABAQUS/Aqua

ABAQUS/Aqua 也是 ABAQUS/Standard 的附加模块，它主要用于海洋工程，可以模拟近海结构，也可以进行海上石油平台导管和立架的分析、基座弯曲的计算和漂浮结构的研究及 J 管道的受拉模拟。它的其他一些功能包括模拟稳定水流和波浪，对受浮力和自由水面上受风载的结构进行分析。本书将不介绍该模块。

- [x] ABAQUS/Foundation

ABAQUS/Foundation 是 ABAQUS/Standard 的一部分，它可以更经济的使用 ABAQUS/Standard 的线性静态和动态分析。本书将不介绍 ABAQUS/Foundation 模块的使用。

- [x] MSC.ADAMS 接口

ABAQUS 的 MSC.ADAMS 接口是基于 ADAMS/Flex 的子模态综合格式，它是 ABAQUS/Standard 的交互产品，使用户能够将 ABAQUS 同机械系统动力学仿真软件 MSC.ADAMS 一起配合使用，可将 ABAQUS 中的有限元模型作为柔性部分输入到 MSC.ADAMS 系列产品中。本书将不介绍该模块。

- [x] MOLDFLOW 接口

ABAQUS 的 MOLDFLOW 接口是 ABAQUS/Explicit 和 ABAQUS/Standard 的交互产品，使用户将注塑成型软件 MOLDFLOW 与 ABAQUS 配合使用，将 MOLDFLOW 分析软件中的有限元模型信息转换成 INP 文件的组成部分。

## Day 49 Abaqus 部件模块（Part）和草图模块（Sketch）
启动 ABAQUS 后，界面中出现 ABAQUS 的第一个功能模块——Part（部件）模块，Part 模块提供了强大的建模功能，支持两种建模方式：在 ABAQUS/CAE 中直接建模和从其他软件中导入模型。

- [x] ABAQUS 中创建部件

单击主菜单上的 Part→Create 命令，或者单击界面工具区，即图 2-1 中的 Create Part（创建部件）工具，将会弹出 Create Part（创建部件）对话框，如图 2-2 所示。
![image](https://user-images.githubusercontent.com/43568675/192106137-a221a952-6c71-4912-a360-f1904713adc3.png)
![image](https://user-images.githubusercontent.com/43568675/192106147-9e2aafa5-891e-4e6c-9385-f050633be3fb.png)


在弹出的 Create Part 对话框中，可以选择调整的是 Name（part 的名称）和 Approximate size（部件的大致尺寸，其单位与模型的单位一致）项，其默认值分别为 Part-n（n 表示创建的第 n 个部件）和 200。其他选项均为单选项，具体介绍如下。

1. Modeling Space：下面有三个选项，如表 2-1 所示。根据所要建立模型的空间结构选择其中的一个。
表 2-1 Modeling Space 选项

2. Options：只有当建立轴对称可变形体时，该选项 Include twist 才被激活，允许轴对称的结构绕对称轴发生扭曲。
3. Typ e：为部件的类型，主要介绍下面三个选项，如表 2-2 所示。
表 2-2 Type 选项
4. Shape：为部件形态，随 Modeling Space 和 Type 选择的变化而变化，如表 2-3 所示。
表 2-3 Shape 选项
5. Type：为建模方式，仅当 Modeling Space 为 3D 且 Type 为 Deformable 或 Discrete rigid 时，该项才可选，如表 2-4 所示。本节将介绍前三种建模方式。
表 2-4 Type 选项

注意可以对部件的特性进行修改，在模型树中单击 Parts 前的，鼠标移至需要修改的 Part 上，单击鼠标右键，在弹出的命令菜单中单击 Edit 命令，弹出 Edit Part 对话框，如图 2-3 所示，可以修改该部件的 Modeling Space、Type 和 Options。

图 2-3 Edit Part 对话框

单击工具区中的 Part Manager（部件管理器）工具，弹出 Part Manager 对话框，如图 2-4 所示，其中列出了模型中的所有部件，可以创建（Create）、复制（Copy）、重命名（Rename）、删除（Delete）、锁定（Lock）、解锁（Unlock）、修正（Update Validity）、忽略操作（Dismiss）。

图 2-4 Part Manager 对话框

设置完图 2-2 中的对话框选项之后，单击 Continue…按钮，进入绘制平面草图的界面，如图 2-5 所示。使用界面左侧工具区中的工具，可以作出点、线、面，作为构成部件的要素（此处不再详细介绍，具体操作可通过相关的例子掌握）。

图 2-5 绘制草图的界面

- [x] 导入部件

可以把建立好的模型导入 ABAQUS 中，导入分为下面两种情况，后面就这两种情况分别加以介绍。
✧ 导入在其他 CAD 软件中建立的模型。
✧ 导入 ABAQUS 建立后导出的模型。ABAQUS 提供了强大的接口，支持 Sketch（草图）、Part（部件）、Assembly（装配件）和 Model（模型）的导入，如图 2-6 所示。
图 2-6 模型的导入菜单

对于每种类型的导入，ABAQUS 都支持多种不同后缀名的文件，但导入的方法和步骤是类似的。另外，还支持 Sketch（草图）、Part（部件）、Assembly（装配）和 VRML（当前视窗的模型导出成 VRML 文件）的导出，如图 2-7 所示。

图 2-7 导出菜单2.1.3 模型的修复与修改有时在导入模型后会出现警告对话框，这是由于导入过程中可能有部分几何元素丢失，使得模型无效或不精确，需要进行修复工作。1．模型的修复有问题的模型在之后的操作中可能会遇到问题，这时需要仔细阅读警告提示的内容，然后单击 Dismiss 按钮。如果出现了警告，则需要对导入的模型进行修复。执行 Tools→Geometry Edit 命令，弹出 Geometry Edit（几何修复工具）对话框，如图 2-8 所示，在 Category（种类）选项中选择需要修复的区域，系统有三个选项可以选择，分别是 Edge（边）、Face（面）、Part（部件），此处选择 Part。
图 2-8 「几何修复工具」对话框Tool 选项与 Category 对应，用于选择几何修复的工具。本例中选择 Convert to precise（转换为精确模型）。单击 Convert to precise 后弹出一个对话框，如图 2-9 所示，再单击 OK 按钮进行几何修复。几何修复工具还可以在工具区调用，用鼠标左键按住工具区中的 Stitch（缝合）工具，展开工具条，单击右侧的 Convert to precise（转换为精确模型）工具，即可进行几何修复。
图 2-9 警告对话框几何修复结束后，可以查看模型。具体操作：单击工具栏中的 Query information（询问信息）工具，弹出 Query 对话框，如图 2-10 所示。
图 2-10 Query 对话框在 Part Module Queries（部件模块询问）中选择 Geometry diagnostics（几何诊断），单击 OK 按钮，弹出 Geometry Diagnostics 对话框，如图 2-11 所示。勾选 Geometry 下的 Imprecise entities 复选框，单击 Highlight 按钮，视图区的模型中以高亮度显示出不精确的部分，如果没有高亮度区，表示该模型已没有不精确的部分。读者可以自行练习 Geometry Diagnostics 对话框中的其他选项。
图 2-11 Geometry Diagnostics 对话框
提示Query information（询问信息）是非常有用的工具，可以对模型的各种信息进行查询。只有 Job 模块没有该工具；除了 Step 和 Load 模块只有 General Queries（一般询问）外，各功能模块都同时包含 General Queries（一般询问）和各自的 Module Queries（模块询问）。读者也可以自行练习。2．模型的修改在创建或导入一个 Part 后，可以使用如图 2-12 所示的工具对此 Part 作一定的修改，实现添加或者切除模型的一部分，以及倒角等功能。
图 2-12 模型修改工具条





## Day 50 流线、迹线和示踪线

流体力学中的流线、迹线和示踪线是描述流场的场线。只有当流场为非稳定状态时，三种场线的形态才会有所区别。反之，对于稳态流场，三种线是相互重合的。

- [x] 流线(Streamlines)：沿着流场质点速度矢量相切的方向形成的连线。所以流线上任意一点切线的方向，就代表了当地流体质点的速度方向。流线的稀疏的地方，流场速度小，流线密集的地方，流场的速度大。而且，每一条流线上的速度和压力的关系，都满足伯努利方程。

- [x] 迹线(Pathlines)：流体质点空间位置在时间历程上形成的轨迹。所以迹线实际上描述的是流场信息在一个时间段内的结果。它记录了不同时刻下跟踪质点空间位置的变化。

- [x] 示踪线（Streaklines）：也有人称之为烟线，定义是所有经过过同一位置的流体质点，在某一时刻下形成的连线。注意是经过过，不是打错字了；他的英文原意是：The loci of points of all the fluid particles that havepassed continuously through a particular spatial point in the past;我们可以这样理解，如果我们在流场中某个点，不断的释放不考虑质量的烟雾或者墨水，那么这些在同一位置点冒出的烟雾和墨水在某一时刻时形成的线，就叫做示踪线。


## Day 51 Abaqus 特性模块（Property）（1）

在 Module（模块）列表中选择 Property（特性），即进入 Property（特性）功能模块，在此模块中可以进行材料和截面特性的设置，以及弹簧、阻尼器和实体表面壳的定义等。进入功能模块后发现主菜单有所变化，如图 2-13 所示，同时工具区转变成与设置材料和截面特性相对应的工具，如图 2-14 所示。

<img width="562" alt="image" src="https://user-images.githubusercontent.com/43568675/192186403-3067e3c6-79e9-4b50-adb5-f2c06618a316.png">

- [x] 定义材料属性

执行 Material→Create 命令，或单击工具区中的 Create Material（创建材料）工具，如图 2-14 所示，弹出 Edit Material（编辑材料）对话框，如图 2-15 所示。对话框包括三个部分。

<img width="451" alt="image" src="https://user-images.githubusercontent.com/43568675/192186432-8bf934fe-a90e-4e61-bc7d-c4de41256733.png">

1. Name（名称）：用于为材料参数命名。
2. Data field（数据区）：出现在 Material Behaviors 的下方，在该区域内设置相应的材料属性值。
3. Material Behaviors（材料性质）：用于选择材料类型。Material Behaviors（材料性质）选择的材料会依次列到下拉菜单的上部。其中包含四个菜单，下面分别对四个菜单项进行介绍。

（1）General：通用特性，如表 2-5 所示。
<img width="570" alt="image" src="https://user-images.githubusercontent.com/43568675/192186479-ec06b42d-8f33-4a5a-8076-7fa546320793.png">

（2）Mechanical：力学特性，如表 2-6 所示。
<img width="543" alt="image" src="https://user-images.githubusercontent.com/43568675/192187213-2593ab13-d72f-444e-976c-fe8695f93ba6.png">


（3）Thermal：热学特性，如表 2-7 所示。
<img width="570" alt="image" src="https://user-images.githubusercontent.com/43568675/192187229-800036c5-2933-49dc-8401-17783168a716.png">


（4）Other：其他特性，如表 2-8 所示。
<img width="581" alt="image" src="https://user-images.githubusercontent.com/43568675/192187240-9f304705-e124-44b6-9d5c-85f42372dad2.png">


注意关于各种类型的材料属性的详细介绍请参阅系统帮助文件《ABAQUS/CAE User's Manual》和《ABAQUS Analysis User's Manual》。


- [x]  创建和分配截面特性

ABAQUS/CAE 不能直接把材料属性赋予模型，而是先创建包含材料属性的截面特性，再将截面特性分配给模型的各区域。

1．创建截面特性单击工具区中的 Create Section（创建截面）工具，弹出 Create Section 对话框，如图 2-16 所示。该对话框包括两部分。
<img width="355" alt="image" src="https://user-images.githubusercontent.com/43568675/192187379-96599964-2819-45ac-96af-25c0ecb21a00.png">

✧ Name（名称）：定义截面的名称。
✧ Category（种类）和 Type（类型）：配合起来指定截面的类型。

（1）Solid（实体）：用于定义实体的截面特性，包括 Homogeneous（均匀体）和 Generalized plane strain（一般平面应变）、Composite（复合的）等，Homogeneous 用于定义二维、三维和轴对称实体的截面特性，Generalized plane strain 用于定义二维平面实体的截面特性。

（2）Shell（壳）：用于定义壳体的截面特性，对应 5 个子选项：Homogeneous（均匀的）、Composite（复合的）、Membrane（膜）、Surface（表面）、General Shell Stiffness（广义壳刚度），其中，Surface 类似于膜，但厚度为零。

（3）Beam（梁）：用于定义梁的截面特性，包括 Beam（梁）和 Truss（桁架）。在创建梁的截面特性前，用户需要先定义梁的横截面的形状和尺寸。

（4）Fluid（流体）：用于定义流体截面性质。

（5）Other（其他）：ABAQUS/CAE 还提供垫圈（Gasket）、黏合层（Cohesive）、声媒介（Acoustic infinite）、声—固耦合（Acoustic interface）的截面特性。

2．分配截面特性创建了截面特性后，就要将它分配给模型。首先，在环境栏的 Part 列表中选择要赋予截面特性的部件，如图 2-17 所示。

<img width="559" alt="image" src="https://user-images.githubusercontent.com/43568675/192187467-d6b59c46-f3ee-4fdb-ac02-24a6eacd17f4.png">

然后单击工具区中的 Assign Section（分配截面）工具，或执行 Assign→Section 命令，按提示在视图区选择要赋予此截面特性的部分，单击提示区的 Done 按钮，弹出 Edit Section Assignment（编辑截面分配）对话框，如图 2-18 所示。该对话框包括以下几项。

<img width="351" alt="image" src="https://user-images.githubusercontent.com/43568675/192187685-b95e21c9-0f77-4120-a4e4-fc93b9a0d458.png">

✧ Create（创建）：当需要分配的截面没有定义时，单击 Create…按钮创建截面。

✧ Section（截面）：用于选择已建立的截面特性，仅列出了与选择区域对应的截面特性。选定后，列表下部会显示出该截面的类型和材料。

✧ Shell Offset（壳偏置）：仅适用于截面类型为 Shell（壳）时，用于设置壳的偏置。

这里需要给出 Cell 的概念，Cell 是 ABAQUS/CAE 中能单独赋予材料和截面属性的最小单元。在建立模型时，可以根据需要选择在基础模型上增加的部分是否是一个 Cell。如果在准备分配截面特性时，发现需要单独分配截面特性的部分没有分离出来，可以选用工具区中适当的 Partition（分割）工具进行部件的分割，如图 2-19 所示。

<img width="295" alt="image" src="https://user-images.githubusercontent.com/43568675/192187764-ce67d312-6a2d-4805-b2a7-ef0d95cfbfcb.png">

✧ Shell Offset（壳偏置）：仅适用于截面类型为 Shell（壳）时，用于设置壳的偏置。这里需要给出 Cell 的概念，Cell 是 ABAQUS/CAE 中能单独赋予材料和截面属性的最小单元。在建立模型时，可以根据需要选择在基础模型上增加的部分是否是一个 Cell。如果在准备分配截面特性时，发现需要单独分配截面特性的部分没有分离出来，可以选用工具区中适当的 Partition（分割）工具进行部件的分割，如图 2-19 所示。

<img width="356" alt="image" src="https://user-images.githubusercontent.com/43568675/192188436-79b376eb-7883-435d-bced-8fd7ecd864a8.png">

提示Partition（分割）工具的功能详见系统帮助文件《ABAQUS/CAE User『 s Manual》。单击工具区的 Section Assignment Manager（截面分配管理器）工具，该管理器中显示已分配的截面列表。

## Day 52 Abaqus 特性模块（Property）2

- [x]  设置梁的截面特性和方向

ABAQUS 还可以在 Property 模块中定义梁的截面特性、截面方向和切向方向。

1．设置梁的截面特性梁的截面特性的设置方法与其他截面类型有所差异，主要体现在以下几个方面。

✧ 在创建梁的截面特性前，需要首先定义梁的横截面的形状和尺寸。
✧ 当选择在分析前提供截面特性时，材料属性在 Edit Beam Section（编辑梁截面）对话框中定义，不需要通过 Create Material 工具创建材料。

2．梁的截面方向和切向方向的设置在分析前，还需要定义梁的截面方向，方法如下。

执行 Assign→Beam Section Orientation 命令，或单击工具区的 Assigning Beam Orientation 工具，在视图区选择要定义截面方向的梁，单击鼠标中键，在提示区中输入梁截面的局部坐标的 1 方向，如图 2-20 所示，按 Enter 键，再单击提示区的 OK 按钮，完成梁截面方向的设置。

<img width="550" alt="image" src="https://user-images.githubusercontent.com/43568675/192188885-1272cdd0-06ad-4e1a-9db2-92247a527b3a.png">

当部件由 Wire（线）组成时，ABAQUS 会默认其切向方向，但可以改变此默认的切向方向。
方法：在主菜单上选择 Assign→Tangent，或单击工具，在展开的工具条中选择 Assigning Beam/Truss Tangent 工具，在视图区选择要改变切向方向的梁，单击提示区的 Done 按钮，梁的切向方向即变为反方向。此时，梁截面的局部坐标的 2 方向也变为反方向。

注意梁截面的局部坐标的 1 方向、2 方向和梁的切向方向满足右手法则。


- [x]  Special 菜单的功能

Property 模块除了能设置材料和截面属性外，还可以通过 Special 菜单进行一些特殊的操作，下面对这些功能进行简单地介绍。

1．Inertia（惯量）根据需要可以定义各种惯量，执行 Special→Inertia→Create 命令，弹出 Create Inertia 对话框，如图 2-21 所示，在 Name 栏中输入名称，在 Type 栏中可以选择 Point mass/inertia（点质量和转动惯量）、Heat capacitance（热容）、Nonstructural mass（非结构质量），单击 Continue…按钮，在视图区选择对象进行相应惯量的设置。

<img width="336" alt="image" src="https://user-images.githubusercontent.com/43568675/192188930-b73e2fea-c4a1-42b9-9e93-cedce3366284.png">

提示惯量的设置详见系统帮助文件《ABAQUS/CAE User's Manual》。

2．Skin（皮肤）在 Property 功能模块中，用户可以在实体模型的面或轴对称模型的边附上一层 Skin（皮肤），适用于几何部件和网格部件。

提示在创建 Skin 之前，需要定义材料和截面属性。Skin 的材料可以不同于其他部件的材料。Skin 的截面类型可以是均匀壳截面（Homogeneous）、膜（Membrane）、复合壳截面（Composite）、表面（Surface）和垫圈（Gasket）。
单击 Special→Skin→Create 命令创建 Skin，详见系统帮助文件《ABAQUS/CAE User's Manual》。一般情况下，不方便直接从模型中选取 Skin，这时可以使用 Set（集合）工具，方法为执行 Tools→Set→Create 命令，在弹出的 Create Set 对话框中输入 name，单击 Continue…按钮，在视图区中选择 Skin 作为构成集合的元素，单击提示区的 Done 按钮，完成集合的定义。单击工具栏的 Create Display Group（创建显示组）工具，在 Item 栏中选择 Sets，在其右侧的区域内选择包含 Skin 的集合，如图 2-22 所示。单击对话框下端的 Intersect（相交）按钮，视图区即显示用户定义的 Skin。

<img width="566" alt="image" src="https://user-images.githubusercontent.com/43568675/192188994-405c0277-4805-48bf-abc8-9237f1ec00a9.png">

注意Skin 不能重叠，仅一个 Skin 能定义在部件的一个指定表面。对于实体和轴对称部件，在 Mesh 功能模块中对部件进行网格划分时，ABAQUS 会自动对位于表面的 Skin 划分对应的网格，而不用单独对 Skin 进行网格划分。

3．Springs/Dashpots（弹簧/阻尼器）ABAQUS 可以定义各种惯量，单击 Special→Springs/Dashpots→Create 命令，弹出 Create Springs/Dashpots 对话框，在 Name 栏中输入名称，在 Connectivity Type 栏中可以选择 Connect two points（连接两点）和 Connect points to ground（连接点和地面），后者仅适用于 ABAQUS/Standard，单击 Continue…按钮，在视图区选择对象进行相应的设置，使用时可以同时设置弹簧的刚度和阻尼器系数。

提示相关内容可参考系统帮助文件《ABAQUS/CAE User's Manual》及《ABAQUS Analysis User's Manual》。
