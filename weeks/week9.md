## Day 53 Abaqus 装配模块（Assembly）1

在 Module（模块）列表中选择 Assembly（装配），即进入 Assembly（装配）功能模块。

在 Part 功能模块中创建或导入部件时，整个过程都是在局部坐标系下进行的。对于由多个部件构成的物体，必须将其在统一的整体坐标系中进行装配，使其成为一个整体，这部分工作在 Assembly 功能模块中进行。

一个模型只能包含一个装配件，一个装配件可以包含多个部件，一个部件也可以被多次调用来组装成装配件。即使装配件中只包含一个部件，也必须进行装配，定义载荷、边界条件、相互作用等操作都必须在装配件的基础上进行。


- [x] 创建部件实体

装配的第一步是选择装配的部件，创建部件实体。具体操作方法如下。

执行 Instance→Create 命令，或单击工具区中的 Instance Part（创建部件实体）工具，弹出 Create Instance 对话框，如图 2-23 所示。

<img width="337" alt="image" src="https://user-images.githubusercontent.com/43568675/192189967-9fd7937d-d812-439e-9646-c98dca506262.png">

该对话框包括三部分，其中，Parts（部件）栏内列出了所有存在的部件，单击鼠标左键进行部件的选取，可以单选，也可以多选，只不过多选时在单击的同时要借助键盘上的 Shift 键或 Ctrl 键。Instance Type（实体类型）选项用于选择创建实体的类型，有两个选项。

✧ Dependent（mesh on part）：用于创建非独立的部件实体，为默认选项。当对部件划分网格时，相同的网格被添加到调用该部件的所有实体中，特别适用于线性阵列和辐射阵列构建部件实体。

✧ Independent（mesh on instance）：该选项用于创建独立的部件实体，这种实体是对原始部件的复制。此时需要对装配件中的每个实体划分网格，而不是原始部件。

提示

与创建非独立的部件实体相比，这种方法会耗用更多的内存；另外，由于节点集合和单元集合被写入每一个独立的部件实体中，这种方法的 Inp 文件也较大。


Auto-offset from other instances 选项用于使实体间产生偏移而不重叠。整体坐标系的原点和坐标轴与第一个部件实体的重合，当继续添加部件实体时，ABAQUS/CAE 会将新实体的坐标系对齐整体坐标系，这样部件实体间可能会产生重叠。

在创建实体前，选中此选项，ABAQUS/CAE 会自动产生偏移而使各实体间无重叠，具体而言，对三维和二维的部件实体产生 X 方向的偏移，对轴对称部件实体产生 Y 方向的偏移。

完成设置后，单击 OK 按钮，完成实体的创建。

提示

工具区和主菜单中没有删除实体等工具，一旦创建部件实体后，可以在模型树中进行这些操作。具体操作：在模型树中单击该模型 Assembly 前的展开该列表，再单击 Instances 前的，鼠标指向需要操作的实体，单击鼠标右键，弹出的命令菜单中的 Delete 按钮用于删除该实体，Suppress 和 Resume 用于抑制和恢复该实体的选择。

部件实体创建完成后，其实体类型可以修改，方法为在模型树中选择该部件实体，单击鼠标右键，在弹出的命令菜单中单击 Make Independent 或 Make Dependent，即可改变实体的类型。


ABAQUS/CAE 还提供以阵列方式复制部件实体，包括线性阵列和辐射阵列两种模式，分别介绍如下。

1．Linear Pattern（线性阵列模式）

执行 Instance→Linear Pattern 命令，或单击工具区的 Linear Pattern（线性阵列模式）工具，在视图区单击鼠标左键选取实体，单击提示区的 Done 按钮，弹出 Linear Pattern 对话框，如图 2-24 所示。该对话框包括以下几项。


<img width="371" alt="image" src="https://user-images.githubusercontent.com/43568675/192190122-9ba9d159-e203-4db6-88b6-0db6a75b73d5.png">


（1）Direction l（方向 1）栏用于设置线性阵列的第一个方向，默认为 X 轴。

✧ Number（数目）：该选项用于设置部件实体的数目（含原始实体），默认值为 2。

✧ Direction（方向）：该选项用于设置线性阵列的方向。单击 Direction...按钮，在视图区中的原始实体上选择一条线段，新实体即按该方向排列。

✧ Offset（偏移）：该选项用于设置实体间的距离。

✧ Flip（反向）：该按钮用于将线性阵列变为反方向。


（2）Direction 2（方向 2）栏用于设置线性阵列的第二个方向，默认为 Y 轴，其选项与 Direction l 完全相同，不再赘述。

（3）Preview（预览）选项用于预览线性阵列的实体，默认为选择预览方式。

完成设置后，单击 OK 按钮，完成线性阵列的实体创建操作。

2．Radial Pattern（辐射阵列模式）

执行 Instance→Radial Pattern 命令，或单击工具区的 Radial Pattern（辐射阵列模式）工具，在视图区单击鼠标左键选取实体，单击提示区的 Done 按钮，弹出 Radial Pattern 对话框，如图 2-25 所示。该对话框包括以下几项。


<img width="357" alt="image" src="https://user-images.githubusercontent.com/43568675/192190187-63a1e4d1-6288-431c-b343-ffa6b5a16f8f.png">

（1）Number（数目）：用于设置阵列实体的数目（含原始实体），默认值为 4，最小可以设置成 2。

（2）Total angle（总角度）：用于设置原始实体与最后一个复制实体间的角度，范围为-360°～360°，正值代表逆时针方向，默认为绕 Z 轴 90°。

（3）Axis（轴）：用于设置辐射阵列的旋转轴，类似于线性阵列中的 Direction 功能。单击 Axis...按钮，在视图区中的原始实体上选择一条线段，新实体即以该线段为轴旋转排列。

（4）Preview（预览）：用于预览辐射阵列的实体，默认为选择预览方式。











## Day 54 Abaqus 装配模块（Assembly）2


- [x]  部件实体的定位
创建了部件实体后，可以采用多种工具对实体进行定位，下面分别进行介绍。

1．平移和旋转工具

使用平移和旋转工具可以完成部件实体在任何情况下的定位，常用工具有 Translate（平移）、Rotate（旋转）、Translate To（平移到）。下面分别对这些工具进行介绍。

（1）Translate（平移）：执行 Instance→Translate 命令，或单击工具区的 Translate Instance（平移实体）工具，在视图区单击鼠标左键选取实体，单击提示区的 Done 按钮。有两种方法实现部件实体的平移。

✧ 按提示输入平移向量起点的坐标，按 Enter 键，继续在提示区输入平移矢量终点的坐标，再次按 Enter 键。

✧ 在视图区中选择部件实体上的一点，接着在视图区中选择部件实体上的另一点。此时，视图区显示出实体移动后的位置，单击 OK 按钮，完成部件实体的移动。

（2）Rotate（旋转）：执行 Instance→Rotate 命令，或单击工具区的 Rotate Instance（旋转实体）工具，在视图区单击鼠标左键选取实体，单击提示区的 Done 按钮。

提示

类似于平移工具，有两种方法确定部件实体的旋转轴。之后，在提示区输入旋转的角度，如图 2-26 所示。范围为-360°～360°，正值表示逆时针方向的旋转，默认为 90°。


<img width="430" alt="image" src="https://user-images.githubusercontent.com/43568675/192454942-202d248c-c835-4256-ac17-c89f76bdad76.png">

输入角度后按 Enter 键，视图区显示出实体旋转后的位置，单击 OK 按钮，完成部件实体的旋转。

（3）Translate To（平移到）：执行 Instance→Translate To 命令，或单击工具区的 Translate To（平移到）工具，在视图区单击鼠标左键选取移动实体的边（二维或轴对称实体）或面（三维实体），单击提示区的 Done 按钮，再选取固定实体的面或边，单击提示区的 Done 按钮。

注意

该工具仅适用于实体模型。

提示

类似于平移工具，选取平移矢量的起止点。之后，需要在提示区输入移动后两实体的间隙距离，如图 2-27 所示。负值表示两实体的重叠距离，默认为 0.0，即选取的两实体的面或边接触在一起，单击 Preview 按钮预览，再单击 Done 按钮确认本次操作。

<img width="443" alt="image" src="https://user-images.githubusercontent.com/43568675/192455000-3f7dff56-4c4d-4dee-88c2-4e5e49fcaa55.png">

如果沿平移矢量的方向，选取的两实体的面或边不能接触在一起，该平移操作将无法进行，并弹出错误提示信息，如图 2-28 所示。


<img width="330" alt="image" src="https://user-images.githubusercontent.com/43568675/192455030-a7b44fcb-4fad-4c5f-bbee-4d337009902f.png">

注意

平移和旋转操作可以预览，但不能撤销或修改，读者可以在预览后再确定是否进行该操作。如果用户觉得实体的平移或旋转不符合要求，可以不断单击提示区的 Go Back to Previous Step（返回上一步）按钮，退回到任一步操作前的状态，再重新进行操作。

2．约束定位工具

ABAQUS/CAE 提供了一系列约束定位工具，包括在 Constraint 菜单和展开工具条中。

提示

这组工具与 Translate To 工具类似，都是通过指定两个部件实体间的位置关系来移动其中一个实体；不同的是约束定位操作可以撤销和修改。下面简要介绍各约束定位工具的功能。

（1）Parallel Face（平行面）：执行 Constraint→Parallel Face 命令，或单击展开工具条的左侧第一个工具，该工具用于使选取的移动实体的平面平行于选取的固定实体的平面。

（2）Parallel Edge（平行边）：执行 Constraint→Parallel Edge 命令，或单击展开工具条的左侧第三个工具，该工具用于使选取的移动实体的直线段平行于选取的固定实体的直线段。

（3）Face to Face（面对面）：执行 Constraint→Face to Face 命令，或单击展开工具条的左侧第二个工具，该工具类似于 Parallel Face 工具，用于使选取的移动实体的平面平行于选取的固定实体的平面，并使两个基准面间产生指定的间距。

（4）Edge to Edge（平行边）：执行 Constraint→Edge to Edge 命令，或单击展开工具条的左侧第四个工具，该工具类似于 Parallel Edge 工具，用于使选取的移动实体的直线段与选取的固定实体的直线段重合。

（5）Coincident Point（重合点）：执行 Constraint→Coincident Point 命令，或单击展开工具条的左侧第六个工具，该工具用于使选取的移动实体上的点与选取的固定实体上的点重合，但移动实体的方向保持不变。

（6）Coaxial（共轴）：执行 Constraint→Coaxial 命令，或单击展开工具条的左侧第五个工具，该工具用于使选取的移动实体的圆柱面或圆锥面平行于选取的固定实体的圆柱面或圆锥面共轴。

（7）Parallel CSYS（平行坐标轴）：执行 Constraint→Parallel CSYS 命令，或单击展开工具条的右侧第一个工具，该工具用于使移动实体上的基准坐标系的轴平行于固定实体上的基准坐标系的轴。

这 7 种工具的操作类似于 Translate To 工具，在此不再赘述，读者可以根据提示区的提示自行练习，系统帮助文件《ABAQUS/CAE User's Manual》。

提示

约束定位工具的操作结果不能进行预览，但可以选择模型树的 Assembly→Position Constraints 命令，将鼠标指向需要修改的操作，单击鼠标右键，在弹出的命令菜单中单击 Edit 按钮，弹出 Edit Feature（编辑特征）对话框，如图 2-29 所示，即可在该对话框中对该约束定位操作进行修改。

<img width="337" alt="image" src="https://user-images.githubusercontent.com/43568675/192459008-0e6ccee8-4e4a-4b18-8c02-f7546e259282.png">

此外，弹出的命令菜单中的 Delete 命令用于删除该约束定位操作，Suppress 和 Resume 命令用于抑制和恢复该约束定位操作。单独的约束定位操作很难对部件实体进行精确定位，往往需要几个约束定位操作的配合才能精确地定位部件实体。

当几个约束定位操作或旋转、平移操作与约束定位操作发生冲突时，可以选择 Instance→Convert Constraints 工具移除模型树中的所有约束定位操作的特征（模型的位置保持不变），之后，再进行平移和旋转操作或新的约束定位操作。

- [x] 合并/剪切部件实体
当装配件包含两个或两个以上的部件实体时，ABAQUS/CAE 提供部件实体的合并（Merge）和剪切（Cut）功能。对选择的实体进行合并或剪切操作后，将产生一个新的实体和一个新的部件。

具体操作：执行 Instance→Merge/Cut 命令，或单击工具区中的 Merge/Cut Instances（合并/剪切实体）工具，弹出 Merge/Cut Instances 对话框，如图 2-30 所示。

<img width="596" alt="image" src="https://user-images.githubusercontent.com/43568675/192459068-bea61e15-8883-4843-94bc-8280cbde996d.png">

该对话框的参数：Part name（部件名称）栏用于输入新生成的部件的名称；Operations（操作）栏用于选择操作的类型。

（1）Merge（合并），用于部件实体的合并。

✧ Geometry（几何）选项用于几何部件实体的合并。

✧ Mesh（网格）选项用于网格实体的合并。

✧ ABAQUS/CAE 可实现网格部件实体和划分了网格的实体部件的合并。Cut geometry（剪切）选项用于部件实体的剪切，仅适用于几何部件实体。

（2）Options（选项），用于设置操作的选项。

✧ Suppress original instances（抑制原始实体）选项用于选择进行合并或剪切操作后，原始实体是否被激活。

✧ Intersecting Boundaries（相交的边界）栏用于选择对部件实体边界的处理，适用于几何部件实体，如图 2-30（a）所示。

✧ Remove（移除）选项用于移除合并的几何部件实体的重合边界，使之成为一个 Cell。

✧ Retain（保留）选项用于保留合并的几何部件实体的公共部分，使之成为三个 Cells。

（3）Merge nodes（合并节点），该栏用于选择节点的合并方式，适用于带有网格的实体，如图 2-30（b）所示。

✧ Boundary only 为默认选项，仅适用于只有一个公共面的情况，此时仅沿边界合并节点。

✧ All 选项适用于部件有重叠时，ABAQUS/CAE 合并选取实体的所有节点。此时，Remove duplicate elements 选项被激活，默认选择该选项，表示移除合并后重合的单元。

✧ None 选项表示不合并节点，ABAQUS/CAE 将保留所有的原始节点。

（4）Tolerance（公差），用于输入合并节点间的最大距离，默认值为 1 × 10−6，即间距在 1 × 10−6内的节点被合并，适用于带有网格的实体，如图 2-30（b）所示。

设置完 Merge/Cut Instances 对话框后，单击 Continue…按钮，视图区选择需要操作的实体，单击提示区的 Done 按钮，ABAQUS/CAE 进行合并或剪切运算，如果操作成功，则会生成一个新的部件实体显示在视图区，而原始实体不再显示在视图区中。此时，在环境栏的 Module 列表中选择 Part，可以看到合并或剪切操作后生成的部件。

注意

若对类型相同的几何部件实体（Dependent 或 Independent）进行合并或剪切操作，则生成同类的实体；若几何部件实体的类型不同，则生成非独立的实体（Dependent）。当对带有网格的实体进行合并或剪切操作时，总是生成非独立的实体（Dependent）。




## Day 54 分析步模块 1
任何几何模型都可在前面介绍的这四个功能模块中创建。Part 模块和 Sketch 模块用于创建部件，Assembly 模块用于组装模型的各部件。

有时，需要将 Part 模块和 Assembly 模块配合起来使用，如通过 Assembly 模块中的合并（Merge）和剪切（Cut）功能创建出新的部件，再进行装配。对装配件中所包含的部件的所有操作都完成后，就可以进入 Step 模块，进行分析步和输出的定义。

- [x] 设置分析步
进入 Step 功能模块后，主菜单中的 Step 菜单及工具区中的 Create Step（创建分析步）工具和 Step Manager（步骤管理器）工具用于分析步的创建和管理。

创建一个模型数据库后，ABAQUS/CAE 默认创建初始步（Initial），位于所有分析步之前。用户可以在初始步中设置边界条件和相互作用，使之在整个分析中起作用，但不能编辑、替换、重命名和删除初始步。

ABAQUS 可以在初始步后创建一个或多个分析步，执行 Step→Create 命令，或单击工具区中的 Create Step（创建分析步）工具，弹出 Create Step 对话框，如图 2-31 所示。


图 2-31 Greate Step 对话框

该对话框包括三部分。

（1）在 Name（名称）栏内输入分析步的名称，默认为 Step-n（n 表示第 n 个创建的分析步）。

（2）Insert new step after 栏用于设置创建的分析步的位置，每个新建立的分析步都可以设置在 Initial（初始步）后的任何位置。

（3）Procedure type（分析步类型）栏用于选择分析步的类型。用户需要首先选择 General（通用分析步）或 Linear perturbation（线性摄动分析步），其下部列表中显示出所有可供选择的分析步类型，默认为 General（通用分析步）中的 Static、General（静态分析）。

✧ General（通用分析步）：用于设置一个通用分析步（General analysis steps），可用于线性分析和非线性分析。该分析步定义了一个连续的事件，即前一个通用分析步的结束是后一个通用分析步的开始。ABAQUS 包括 13 种通用分析步，如表 2-9 所示。

表 2-9 通用分析步


✧ Linear perturbation（线性摄动分析步）：用于设置一个线性摄动分析步（Linear perturbation analysis steps），仅适用于 ABAQUS/Standard 中的线性分析。ABAQUS 包括 10 种线性摄动分析步，如表 2-10 所示。

表 2-10 线性摄动分析步


选择分析类型后，单击 Continue…按钮，弹出 Edit Step（编辑分析步）对话框。对于不同类型的分析步，该对话框的选项有所差异。下面就几种常用的分析步进行介绍。

1．Static General（静力学分析）分析步

该分析步用于分析线性或非线性静力学问题，其 Edit Step 对话框包括 Basic、Incrementation 和 Other 三个选项卡页面。

（1）Basic（基础）选项卡，该页面主要用于设置分析步的时间和大变形等，如图 2-32 所示。


图 2-32 编辑分析步的 Basic 选项卡页面

✧ Description（描述）：用于输入对该分析步的简单描述，该描述保存在结果数据库中，进入 Visualization 模块后显示在状态区。该栏非必选项，用户可以不对分析步进行描述。

✧ Time period（时间）：用于输入该分析步的时间，系统默认值为 1。对于一般的静力学问题，可以采用默认值。

✧ Nlgeom：用于选择该分析步是否考虑几何非线性，对于 ABAQUS/Standard 该选项默认为 Off（关闭）。

✧ Use stabilization with：该选项用于局部不稳定的问题（如表面褶皱、局部屈曲），ABAQUS/Standard 会施加阻尼来使该问题变得稳定。

✧ Include adiabatic heating effects：用于绝热的应力分析，如高速加工过程。

（2）Incrementation（增量）选项卡页面，该页面用于设置增量步，如图 2-33 所示。


图 2-33 编辑分析步的 Incrementation 选项卡页面

✧ Type（类型）：该选项用于选择时间增量的控制方法，包括两种方式：Automatic（自动的）为默认选项，ABAQUS/Standard 根据计算效率来选择时间增量。

提示

建议读者采用这种方式。Fixed（固定的）选项，ABAQUS/Standard 采用设置的固定的时间增量进行运算。在确保所设的时间增量能够收敛的情况下，可以选择该选项。

✧ Maximum number of increments（增量步的最大数目）：该栏用于设置该分析步的增量步数目的上限，默认值为 100。即使没有完成分析，当增量步的数目达到该值时，分析停止。

✧ Increment size（时间增量大小）：该栏用于设置时间增量的大小。当选择 Automatic 时，用户可以设置 Initial（初始时间增量）、Minimum（最小的时间增量）和 Maximum（最大的时间增量），默认值分别为 l、1×10−5和 1。当选择 Fixed 时，只能设置时间增量的大小。

（3）Other（其他）选项卡页面，该页面用于选择求解器、求解技巧、载荷随时间的变化等，如图 2-34 所示。


图 2-34 编辑分析步的 Other 选项卡页面

✧ Equation Solver（求解器）：用于选择求解器和矩阵存储方式，如表 2-11 所示。

表 2-11 Equation Solver 选项


✧ Solution Technique（求解技巧）：用于选择非线性平衡方程组的求解技巧，如表 2-12 所示。

表 2-12 Solution Technique 选项


表 2-13 Convert severe discontinuity iterations 选项


✧ Convert severe discontinuity iterations：用于选择非线性分析中高度不连续迭代的处理方法，如表 2-13 所示。

✧ Default load variation with time：用于选择载荷随时间的改变方式，如表 2-14 所示。

表 2-14 Default load variation with time 选项


✧ Extrapolation of previous state at start of each increment：用于选择每个增量步开始时的外推方法，ABAQUS/Standard 采用外推法加速非线性分析的收敛，如表 2-15 所示。

表 2-15 Extrapolation of previous state at start of each increment 选项


✧ Stop when region is fully plastic：若指定区域内所有计算点的解答是完全塑性的，该分析步结束。

✧ Obtain long-term solution with time-domain material properties：适用于黏弹性或黏塑性材料。

✧ Accept solution after reaching maximum number of iterations：当在 Incrementation 选项卡页面中选择 Fixed 时间增量时，该选项可以被选择。若选择该选项，当增量步达到设置的上限数目时，ABAQUS/Standard 接受此时的解答。建议不选择此选项。

2．Dynamic，Implicit（隐式动力学分析）分析步

该分析卡用于分析线性或非线性隐式动力学分析问题，其 Edit Step 对话框也包括 Basic、Incrementation 和 Other 三个选项卡页面，其中很多选项与静力学分析时相同，此处仅介绍不同的选项。

在 Incrementation（增量）页面中，当选择自动时间增量（Automatic）时，可以设置 Half-step residual tolerance（增量步中的平衡残余误差的容差）；当选择固定时间增量（Fixed）时，可以选择 Suppress half-step residual calculation 来加快收敛。Other（其他）选项卡页面的参数说明如下。

（1）Solution Technique（求解技巧）中不包括 Contact iterations（接触迭代方法）。

（2）Numerical damping control parameter（数值阻尼控制参数）：该栏用于输入数值阻尼控制参数，范围为 0～-0.333（阻尼），默认值为-0.05。

（3）Default load variation with time 的默认选项为 Instantaneous（瞬间加载）。

（4）By pass calculations of initial accelerations at the beginning of step：适用于分析步开始时载荷不突然变化的情况，ABAQUS/Standard 在分析步开始时不计算初始加速度。若前一个分析步也是动力学分析步，采用前一个分析步结束时的加速度作为新的分析步的加速度。若当前分析步是第一个动力学分析步，加速度为 0；在默认情况下，ABAQUS/Standard 计算初始加速度。

3．Dynamic，Explicit（显式动力学分析）分析步

该分析步用于显式动力学分析，除 Basic、Incrementation 和 Other 三个选项卡页面外，Edit Step 对话框中还包括一个 Mass scaling 选项卡页面。

Basic（基础）选项卡页面中的 Nlgeom 选项默认为 On（开）。Incrementation（增量）选项卡页面的相关参数如表 2-16 所示。

表 2-16 Incrementation 选项卡


（1）Mass scaling（质量缩放）选项卡页面用于质量缩放的定义。当模型的某些区域包含控制稳定极限的很小的单元时，ABAQUS/Explicit 采用质量缩放功能来增加稳定极限，提高分析效率。

✧ 「Use scaled mass andthroughout step」definitions from the previous step：为默认选项，程序采用前一个分析步对质量缩放的定义。

✧ Use scaling definitions below：用于创建一个或多个质量缩放定义。单击该对话框下部的 Create…按钮，弹出 Edit Mass Scaling 对话框，如图 2-35 所示，在该对话框内选择质量缩放的类型并进行相应的设置。


图 2-35 Edit Mass Scaling 对话框

设置完成后，Edit Step 对话框的 Data 列表内将显示出该质量缩放的设置，用户可以单击该对话框下部的 Edit…或 Delete 按钮进行质量缩放定义的编辑或删除，如图 2-36 所示。


图 2-36 设置质量缩放后的 Edit Step 对话框

说明

这里不详细讲解 Edit Mass Scaling 对话框的使用，请参阅系统帮助文件《ABAQUS/CAE User's Manual》。

（2）Other（其他）选项卡页面，不同于 Static，General 和 Dynamic，Implicit 的情况，该页面仅包含 Linear bulk viscosity parameter 和 Quadratic bulk viscosity parameter 两栏，如图 2-37 所示。


图 2-37 Edit Step 对话框中的 Other 标签栏图

Linear bulk viscosity parameter：用于输入线性体积黏度参数，默认值为 0.06，ABAQUS/Explicit 默认使用该类参数。

Quadratic bulk viscosity parameter：用于输入二次体积黏度参数，默认值为 1.2，仅适用于连续实体单元和压容积应变率时。

4．Static，Linear perturbation（线性摄动静力学分析）分析步

该分析步用于线性静力学分析，其 Edit Step 对话框仅包含 Basic 和 Other 两个选项卡页面，如图 2-38 所示，且选项为 Static，General 的子集。


图 2-38 线性摄动静力学分析中的 Edit Step 对话框

（1）Basic（基础）选项卡页面：仅包含 Description（描述）栏。Nlgeom 为 Off（关闭），即不涉及几何非线性问题。

（2）Other（其他）选项卡页面：仅包含 Equation Solver（求解器）栏。

设置完 Edit Step 对话框后，单击 OK 按钮，完成分析步的创建。此时单击工具区 Step Manager（步骤管理器）工具，可见步骤管理器内列出了初始步和已创建的分析步，可以对列出的分析步进行编辑、替换、重命名、删除操作和几何非线性的选择，如图 2-39 所示。另外，环境栏的 Step 列表中也列出了初始步和已创建的分析步。


图 2-39 步骤管理器

这里只介绍这四种常用的分析步，读者若想了解其他分析步的设置，请参阅系统帮助文件《ABAQUS/CAE User's Manual》和《ABAQUS Analysis User's Manual》。

注意

ABAQUS 对分析步的数量没有限制，但严格限制其排列顺序。当继续创建分析步时，Create Step 对话框的分析步列表自动更新，仅列出可以选用的分析步。



















- [x] 定义输出
用户可以设置写入输出数据库的变量，包括场变量（以较低的频率将整个模型或模型的大部分区域的结果写入输出数据库）和历史变量（以较高的频率将模型的小部分区域的结果写入输出数据库）。

1．变量输出要求管理器

创建了分析步后，ABAQUS/CAE 会自动创建默认的场变量输出要求和历史变量输出要求（线性摄动分析步中的 Buckle、Frequency.Complex Frequency 无历史变量输出）。

单击工具区中 Field Output Manager（场变量输出要求管理器）工具和 Field History Manager（历史变量输出要求管理器）工具，分别弹出场变量输出要求管理器和历史变量输出要求管理器，图 2-40 所示为创建如图 2-39 所示的分析步后的场变量输出要求管理器和历史变量输出要求管理器。


图 2-40 输出要求管理器

提示

这两个管理器的布局完全相同，下面只介绍场变量输出要求管理器，历史变量输出要求管理器的使用与之相同。

ABAQUS 可以在场变量输出要求管理器中进行场变量输出要求的创建、重命名、复制、删除、编辑。此外，列表最左侧的表示该场变量输出要求被激活，单击此图标则变为，表示该场变量输出要求被抑制。

提示

这些功能也可以执行 Output→Field Output Requests 和 Output→History Output Requests 命令。

已创建的通用分析步的场变量输出要求，在之后所有的通用分析步中继续起作用，在管理器中显示为 Propagated，如图 2-40（a）所示。

单击管理器中 Step-3 下的 Propagated，右侧的 Deactivate 变为可选按钮，单击该按钮，Propagated 变为 Inactive，表明 Step-1 创建的场变量输出要求在 Step-3 中不起作用。此时 Activate 变为可选按钮，可用于激活 Step-3 的场变量输出要求。该功能同样适用于线性摄动分析步，但必须是同一种线性摄动分析步的场变量输出要求。

提示

若在所有通用分析步前创建一个通用分析步，则 ABAQUS/CAE 不会自动创建一个默认的场变量输出要求。此时可以使用 Move Left 和 Move Right 来控制场变量输出要求起作用的范围，也可以创建一个新的场变量输出要求。该功能同样适用于线性摄动分析步，但必须是同一种线性摄动分析步的场变量输出要求。

注意

如果有的分析步不包含场变量输出要求，ABAQUS/CAE 在生成 inp 文件时会出现警告。

2．编辑输出要求

单击场变量输出要求管理器或历史变量输出要求管理器中的 Edit…按钮，弹出 Edit Field Output Request 或 Edit History Output Request 对话框，如图 2-41 所示，就可以对场变量输出要求/历史变量输出要求进行修改。


图 2-41 编辑变量输出要求

1）编辑场变量输出要求

在 Edit Field Output Request 对话框中，用户可以对场变量输出要求进行设置。不同分析步的选项可能不完全相同，下面以 Static，General 分析步为例进行介绍。

✧ Domain（范围）：该列表用于选择输出变量的区域，如表 2-17 所示。

表 2-17 Domain 选项


✧ Frequency（频率）：该栏用于设置输出变量的频率，如表 2-18 所示。

表 2-18 Frequency 选项


✧ Timing：当在 Frequency 列表中选择 Every x units of time、Evenly spaced time intervals 或 From time points 时，该列表为可选，包括 Output at exact times（在精确时间输出）和 Output at approximate times（在近似的时间输出）。

✧ Output Variables（输出变量）：用于选择写入输出数据库的场变量，可通过几种方式进行选择：Select from list below（从列表中选择）、All（全选）、Preselected defaults（默认选择）、Edit variables（编辑变量名称）。输出变量列表与输出变量的区域选择相对应。这是需要重点选择的部分，写入输出数据库的场变量越多，输出数据库占的计算机空间也相应地增大，所以用户应该根据需要选择输出变量。

✧ Output for rebar：用于选择写入输出数据库的场变量中是否包括钢筋的结果，Domain 中为 Whole model 或 Set 时被激活。

✧ Output at shell，beam，and layered section points：用于设置写入输出数据库的场变量的截面点，Domain 中为 Whole model 或 Set 时被激活。

✧ Include local coordinate directions when available：不选择该项可以减小输出数据库，默认为选择该项。

完成设置后，单击 OK 按钮。

2）编辑历史变量输出要求

Edit History Output Request 对话框与 Edit Field Output Request 对话框基本相同，现就其不同之处进行介绍（仍以 Static，General 分析步为例）。

✧ Domain（范围）中增加了 Springs/Dashpots（将指定的弹簧/阻尼器的场变量写入输出数据库）和 Contour integral（将指定的围线积分中的场变量写入输出数据库）。

✧ 不包含 Include local coordinate directions when available 选项。

2.4.3 Step 模块的其他功能
Step 模块除了能够设置分析步和定义输出变量外，还能通过 Output 菜单和 Other 菜单进行其他操作，下面简单进行介绍。

1．ALE 自适应网格

ALE 自适应网格适用于静力学分析（Static，General）、热—力耦合分析（Coupled temp-displacement）、显式动力学分析（Dynamic，Explicit）、显式动态温度—位移耦合分析（Dynamic，Temp-disp，Explicit）、土壤力学分析（Soils）。

ALE 自适应网格（ALE adaptive meshing）是任意拉格朗日—欧拉（Arbitrary Lagrangian-Eulerian）分析，它综合了拉格朗日分析和欧拉分析的特征，在整个分析中保持高质量的网格而不改变网格的拓扑结构。

主菜单中的 Other 下有三个子菜单用于 ALE 自适应网格。

（1）Other→ALE Adaptive Mesh Domain 菜单用于指定模型中 ALE 自适应网格的区域，一个分析步只能指定一个区域。

（2）Other→ALE Adaptive Mesh Constraint 菜单用于指定 ALE 自适应网格的约束。

（3）Other→ALE Adaptive Mesh Controls 菜单用于指定 ALE 自适应网格的控制。

若想进一步了解 ALE 自适应网格，请参阅系统帮助文件《ABAQUS/CAE User's Manual》和《ABAQUS Analysis User's Manual》。

2．求解控制

通过调整参数可以控制 ABAQUS 的分析，包括通用求解控制和线性方程组迭代求解器的控制。Other→General Solution Controls 菜单用于通用求解控制，仅适用于 ABAQUS/Standard 的通用分析步，用户通过调整变量来控制收敛和时间积分的精确性。

提示

请参阅系统帮助文件《ABAQUS/CAE User's Manual》和《ABAQUS Analysis User's Manual》。

Other→Solver Controls 菜单用于线性方程组迭代求解器的控制，适用于通用静力学分析（Static，General）、线性摄动静力学分析（Static，Linear perturbation）、黏性分析（Visco）和传热分析（Heat transfer）。详见系统帮助文件《ABAQUS/CAE User's Manual》和《ABAQUS Analysis User's Manual》。

注意

读者要慎用通用求解控制，因为通用求解控制的默认设置适用于大多数分析，改变默认设置可能增加计算时间、产生不精确的解或导致收敛问题。

3．特殊的输出

在 Step 模块中，除了能设置场变量输出要求和历史变量输出要求外，还能进行特殊的输出控制，这些功能都包含在 Output 菜单中，详见系统帮助文件《ABAQUS/CAE User's Manual》。


ABAQUS 基础入门与案例精通
作者：张建华 丁磊编著
扫码下载知乎APP 客户端



