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

ABAQUS 的 MOLDFLOW 接口是 ABAQUS/Explicit 和 ABAQUS/Standard 的交互产品，使用户将注塑成型软件 MOLDFLOW 与 ABAQUS 配合使用，将 MOLDFLOW 分析软件中的有限元模型信息转换成 INP 文件的组成部分。本书将不介绍该模块。



