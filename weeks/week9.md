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




## Day 55 分析步模块（STEP） 1
任何几何模型都可在前面介绍的这四个功能模块中创建。Part 模块和 Sketch 模块用于创建部件，Assembly 模块用于组装模型的各部件。

有时，需要将 Part 模块和 Assembly 模块配合起来使用，如通过 Assembly 模块中的合并（Merge）和剪切（Cut）功能创建出新的部件，再进行装配。对装配件中所包含的部件的所有操作都完成后，就可以进入 Step 模块，进行分析步和输出的定义。

- [x] 设置分析步
进入 Step 功能模块后，主菜单中的 Step 菜单及工具区中的 Create Step（创建分析步）工具和 Step Manager（步骤管理器）工具用于分析步的创建和管理。

创建一个模型数据库后，ABAQUS/CAE 默认创建初始步（Initial），位于所有分析步之前。用户可以在初始步中设置边界条件和相互作用，使之在整个分析中起作用，但不能编辑、替换、重命名和删除初始步。

ABAQUS 可以在初始步后创建一个或多个分析步，执行 Step→Create 命令，或单击工具区中的 Create Step（创建分析步）工具，弹出 Create Step 对话框，如图 2-31 所示。

<img width="638" alt="image" src="https://user-images.githubusercontent.com/43568675/192687413-440e8905-4ecf-493e-aede-ba0b478edc42.png">

该对话框包括三部分。

（1）在 Name（名称）栏内输入分析步的名称，默认为 Step-n（n 表示第 n 个创建的分析步）。

（2）Insert new step after 栏用于设置创建的分析步的位置，每个新建立的分析步都可以设置在 Initial（初始步）后的任何位置。

（3）Procedure type（分析步类型）栏用于选择分析步的类型。用户需要首先选择 General（通用分析步）或 Linear perturbation（线性摄动分析步），其下部列表中显示出所有可供选择的分析步类型，默认为 General（通用分析步）中的 Static、General（静态分析）。

✧ General（通用分析步）：用于设置一个通用分析步（General analysis steps），可用于线性分析和非线性分析。该分析步定义了一个连续的事件，即前一个通用分析步的结束是后一个通用分析步的开始。ABAQUS 包括 13 种通用分析步，如表 2-9 所示。

<img width="984" alt="image" src="https://user-images.githubusercontent.com/43568675/192687356-cbcbbb3b-f01e-4816-8ce3-ada022387bd7.png">


✧ Linear perturbation（线性摄动分析步）：用于设置一个线性摄动分析步（Linear perturbation analysis steps），仅适用于 ABAQUS/Standard 中的线性分析。ABAQUS 包括 10 种线性摄动分析步，如表 2-10 所示。

<img width="991" alt="image" src="https://user-images.githubusercontent.com/43568675/192687467-df0a8e68-4e25-4130-bb24-605abb879eda.png">

选择分析类型后，单击 Continue…按钮，弹出 Edit Step（编辑分析步）对话框。对于不同类型的分析步，该对话框的选项有所差异。下面就几种常用的分析步进行介绍。

1．Static General（静力学分析）分析步

该分析步用于分析线性或非线性静力学问题，其 Edit Step 对话框包括 Basic、Incrementation 和 Other 三个选项卡页面。

（1）Basic（基础）选项卡，该页面主要用于设置分析步的时间和大变形等，如图 2-32 所示。


✧ Description（描述）：用于输入对该分析步的简单描述，该描述保存在结果数据库中，进入 Visualization 模块后显示在状态区。该栏非必选项，用户可以不对分析步进行描述。

✧ Time period（时间）：用于输入该分析步的时间，系统默认值为 1。对于一般的静力学问题，可以采用默认值。

✧ Nlgeom：用于选择该分析步是否考虑几何非线性，对于 ABAQUS/Standard 该选项默认为 Off（关闭）。

✧ Use stabilization with：该选项用于局部不稳定的问题（如表面褶皱、局部屈曲），ABAQUS/Standard 会施加阻尼来使该问题变得稳定。

✧ Include adiabatic heating effects：用于绝热的应力分析，如高速加工过程。

（2）Incrementation（增量）选项卡页面，该页面用于设置增量步，如图 2-33 所示。

<img width="832" alt="image" src="https://user-images.githubusercontent.com/43568675/192687562-fb96a23e-9bbd-4aed-a66d-b5e509e94669.png">

✧ Type（类型）：该选项用于选择时间增量的控制方法，包括两种方式：Automatic（自动的）为默认选项，ABAQUS/Standard 根据计算效率来选择时间增量。

提示

建议读者采用这种方式。Fixed（固定的）选项，ABAQUS/Standard 采用设置的固定的时间增量进行运算。在确保所设的时间增量能够收敛的情况下，可以选择该选项。

✧ Maximum number of increments（增量步的最大数目）：该栏用于设置该分析步的增量步数目的上限，默认值为 100。即使没有完成分析，当增量步的数目达到该值时，分析停止。

✧ Increment size（时间增量大小）：该栏用于设置时间增量的大小。当选择 Automatic 时，用户可以设置 Initial（初始时间增量）、Minimum（最小的时间增量）和 Maximum（最大的时间增量），默认值分别为 l、1×10−5和 1。当选择 Fixed 时，只能设置时间增量的大小。

（3）Other（其他）选项卡页面，该页面用于选择求解器、求解技巧、载荷随时间的变化等，如图 2-34 所示。

<img width="567" alt="image" src="https://user-images.githubusercontent.com/43568675/192706472-d1b4294f-c877-4046-a99f-d3819e7755ec.png">


✧ Equation Solver（求解器）：用于选择求解器和矩阵存储方式，如表 2-11 所示。

<img width="645" alt="image" src="https://user-images.githubusercontent.com/43568675/192706448-3a24883d-fecc-4478-a14c-ea6f1a154115.png">


✧ Solution Technique（求解技巧）：用于选择非线性平衡方程组的求解技巧，如表 2-12 所示。

<img width="1033" alt="image" src="https://user-images.githubusercontent.com/43568675/192688001-074b7e38-8800-464a-bbf8-ddf254283671.png">





✧ Convert severe discontinuity iterations：用于选择非线性分析中高度不连续迭代的处理方法，如表 2-13 所示。
<img width="561" alt="image" src="https://user-images.githubusercontent.com/43568675/192706513-a157ff10-0569-484a-85fb-a0cd35d25716.png">

✧ Default load variation with time：用于选择载荷随时间的改变方式，如表 2-14 所示。
<img width="546" alt="image" src="https://user-images.githubusercontent.com/43568675/192706556-75529c1d-3f86-4a12-a2db-4f1d0c06e18f.png">




✧ Extrapolation of previous state at start of each increment：用于选择每个增量步开始时的外推方法，ABAQUS/Standard 采用外推法加速非线性分析的收敛，如表 2-15 所示。

<img width="559" alt="image" src="https://user-images.githubusercontent.com/43568675/192707131-69ee8fca-1dce-4846-9ae4-3645b6cd883a.png">


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

<img width="592" alt="image" src="https://user-images.githubusercontent.com/43568675/192707204-24681c6e-71fb-4251-9c38-503b6f953e01.png">


（1）Mass scaling（质量缩放）选项卡页面用于质量缩放的定义。当模型的某些区域包含控制稳定极限的很小的单元时，ABAQUS/Explicit 采用质量缩放功能来增加稳定极限，提高分析效率。

✧ 「Use scaled mass andthroughout step」definitions from the previous step：为默认选项，程序采用前一个分析步对质量缩放的定义。

✧ Use scaling definitions below：用于创建一个或多个质量缩放定义。单击该对话框下部的 Create…按钮，弹出 Edit Mass Scaling 对话框，如图 2-35 所示，在该对话框内选择质量缩放的类型并进行相应的设置。

<img width="333" alt="image" src="https://user-images.githubusercontent.com/43568675/192707247-d3b9b52f-73e4-40a5-be57-515ee03e8fbb.png">

设置完成后，Edit Step 对话框的 Data 列表内将显示出该质量缩放的设置，用户可以单击该对话框下部的 Edit…或 Delete 按钮进行质量缩放定义的编辑或删除，如图 2-36 所示。


<img width="440" alt="image" src="https://user-images.githubusercontent.com/43568675/192707295-9d7a1ae1-c0d7-4c66-9bb5-3568c07f477e.png">

说明

这里不详细讲解 Edit Mass Scaling 对话框的使用，请参阅系统帮助文件《ABAQUS/CAE User's Manual》。

（2）Other（其他）选项卡页面，不同于 Static，General 和 Dynamic，Implicit 的情况，该页面仅包含 Linear bulk viscosity parameter 和 Quadratic bulk viscosity parameter 两栏，如图 2-37 所示。


<img width="483" alt="image" src="https://user-images.githubusercontent.com/43568675/192707337-02fa916d-deb0-427c-8dc2-a91a3206d9c5.png">

Linear bulk viscosity parameter：用于输入线性体积黏度参数，默认值为 0.06，ABAQUS/Explicit 默认使用该类参数。

Quadratic bulk viscosity parameter：用于输入二次体积黏度参数，默认值为 1.2，仅适用于连续实体单元和压容积应变率时。

4．Static，Linear perturbation（线性摄动静力学分析）分析步

该分析步用于线性静力学分析，其 Edit Step 对话框仅包含 Basic 和 Other 两个选项卡页面，如图 2-38 所示，且选项为 Static，General 的子集。


<img width="423" alt="image" src="https://user-images.githubusercontent.com/43568675/192707372-7842e8c9-4ec8-4dfa-ba1c-2616c4ecfed8.png">

（1）Basic（基础）选项卡页面：仅包含 Description（描述）栏。Nlgeom 为 Off（关闭），即不涉及几何非线性问题。

（2）Other（其他）选项卡页面：仅包含 Equation Solver（求解器）栏。

设置完 Edit Step 对话框后，单击 OK 按钮，完成分析步的创建。此时单击工具区 Step Manager（步骤管理器）工具，可见步骤管理器内列出了初始步和已创建的分析步，可以对列出的分析步进行编辑、替换、重命名、删除操作和几何非线性的选择，如图 2-39 所示。另外，环境栏的 Step 列表中也列出了初始步和已创建的分析步。


<img width="480" alt="image" src="https://user-images.githubusercontent.com/43568675/192707396-62f0ce97-55ca-401e-81a1-cdf2eda9b7c8.png">

这里只介绍这四种常用的分析步，读者若想了解其他分析步的设置，请参阅系统帮助文件《ABAQUS/CAE User's Manual》和《ABAQUS Analysis User's Manual》。

注意

ABAQUS 对分析步的数量没有限制，但严格限制其排列顺序。当继续创建分析步时，Create Step 对话框的分析步列表自动更新，仅列出可以选用的分析步。




## Day 55 分析步模块（STEP） 2


- [x] 定义输出
用户可以设置写入输出数据库的变量，包括场变量（以较低的频率将整个模型或模型的大部分区域的结果写入输出数据库）和历史变量（以较高的频率将模型的小部分区域的结果写入输出数据库）。

1．变量输出要求管理器

创建了分析步后，ABAQUS/CAE 会自动创建默认的场变量输出要求和历史变量输出要求（线性摄动分析步中的 Buckle、Frequency.Complex Frequency 无历史变量输出）。

单击工具区中 Field Output Manager（场变量输出要求管理器）工具和 Field History Manager（历史变量输出要求管理器）工具，分别弹出场变量输出要求管理器和历史变量输出要求管理器，图 2-40 所示为创建如图 2-39 所示的分析步后的场变量输出要求管理器和历史变量输出要求管理器。

<img width="1054" alt="image" src="https://user-images.githubusercontent.com/43568675/192938918-7985e18a-47ba-4d14-a3a6-b73efa39a6fd.png">

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

<img width="1089" alt="image" src="https://user-images.githubusercontent.com/43568675/192939293-dde6afed-de07-497b-98d1-ce09b0a84d15.png">


1）编辑场变量输出要求

在 Edit Field Output Request 对话框中，用户可以对场变量输出要求进行设置。不同分析步的选项可能不完全相同，下面以 Static，General 分析步为例进行介绍。

✧ Domain（范围）：该列表用于选择输出变量的区域，如表 2-17 所示。

<img width="1112" alt="image" src="https://user-images.githubusercontent.com/43568675/192939312-12d68d78-ccc0-4dba-8641-c31d131a03b4.png">


✧ Frequency（频率）：该栏用于设置输出变量的频率，如表 2-18 所示。

<img width="1096" alt="image" src="https://user-images.githubusercontent.com/43568675/192939372-1cca5ee3-f40e-4a24-83eb-575faa56069e.png">


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


- [x]  Step 模块的其他功能
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

## Day 57 fluent湍流模型
涡粘模型(基于雷诺平均NS方程- RANS)
    SA(单方程模型，1994)
        优点:单方程求解，所以计算量小，对解决复杂的边界问题有较好的效果。 
        局限性:对三维流、自由剪切流、强分离流模拟较差、不能预测各向同性湍流的耗散 
        适用范围:不太复杂的流动(准二维)，如翼型、机翼、机身、导弹、船身等
    k-epsilon(k-ε，二方程模型)近壁面采用壁面 函数法、壁面处理精度不足(一般用于Re比较大 时)
        Standrad:
             优点:工业应用广泛(模型参数通过实验数据验证过)
            局限性: 
                 a.对有大的压力梯度、强分离流、强旋流和大曲率流动，模拟 精度不够
                 b.难以准备模拟出射流的传播 
                c.对有大的应变区域(如近分 离点)，模拟的k偏大
            适用范围:管流、平板流、适用于压缩性、浮力、燃烧等子模型 
        Realizable
            局限性:强旋转精度不够
            优点:
                 精确预测平板和圆柱射流的传播
                对包括旋转、有大反压力梯度的边界层、分离、回流等现象有更好的预测结果
        RNG
            优点:修正了耗散率方程、在一些复杂的剪切流、有大应变
            率、旋涡、分离等流动问题比SKE 表现更好
    k-omega(k–ω)直接求解边界层网格数据、近壁 面处理好，对于逆压力梯度和分离流动精度较好
        Standard:
               对封闭腔内边界层、自由剪切流、低雷诺数流模拟   较好，适合有反向压力梯度和分离的复杂边界层(   外气动和旋转机械)，可用于转捩流动。一般预测   的分离点过早。
                转捩(lie)流(transition flow)是层流向湍 流(紊流)转化过程中的一种流动状态。而这种 转化现象，称为转捩。
            一般时不建议采用，对ω较为敏感 Low-Re:近壁面精度较好
        Low-Re:近壁面精度较好
        GEKO:
        BSL
            优点:近壁面采用k-omega，主流区采用k- epsilon,
            局限性:计算量大
        SST
            优点:基于BSL的改良，简化了模型，减小计算量
            局限性:由于对壁面距离的敏感，不太适合自由剪切流
    Reynolds Stress
        物理上是最可靠的RANS 模型，克服了涡粘模型 的各向同性假设。需要更多的CPU时间和内存， 由于方程间强耦合性，收敛稍差。适合复杂三维 流动，强旋流等，如旋流燃烧器，旋风分离器等

## Day 58 载荷模块（Load）1

进入 Load 功能模块后，主菜单中的 Load 菜单及工具区中的 Create Load（创建载荷）工具和 Load Manager（载荷管理器）工具用于载荷的创建和管理。

- [x]  定义载荷

定义载荷时，执行 Load→Create 命令，或单击工具区中的 Create Load（创建载荷）工具，也可双击左侧模型树中的 Loads，弹出 Create Load 对话框，如图 2-42 所示。该对话框包括以下几项。


![image](https://user-images.githubusercontent.com/43568675/193416118-28795202-184c-4621-aa87-cff0a28361e6.png)


（1）Name（名称），在该栏内输入载荷的名称，默认为 Load-n（n 为第 n 个创建的

（2）Step（分析步），该列表用于选择用于创建载荷的分析步。


注意

在初始步（Initial）中不能定义载荷，必须在 Step 列表中选择分析步施加相应的载荷。

（3）Category（种类），用于选择适用于所选分析步的加载种类，包括 Mechanical（力学的）、Fluid（流体）、Thermal（热学的）、Acoustic（声学的）、Electrical（电学的）、Mass diffusion（质量扩散）。对于不同的分析步，可以施加不同的载荷种类。

（4）Types for Selected Step，用于选择载荷的类型，是 Category 的下一级选项。

✧ Mechanical：包括 Concentrated force（集中力）、Moment（力矩）、Pressure（施加在面上的压力载荷）、Surface traction（施加在面上的载荷）、Shell edge load（施加在壳边上的载荷）、Pipe pressure（管道压力）、Line load（施加在梁上的线载荷）、Body force（体力）、Gravity（重力，输入指定方向的加速度）、Generalized plane strain（广义平面应变）、Rotational body force（旋转体力），Bolt load（螺栓或扣件的预紧力）、Coriolis force（科氏力）、Connector force（施加在连接器上的集中力）、Inertia Relief（惯性释放载荷）、Connector moment（施加在连接器上的力矩），如图 2-42（a）所示。

✧ Thermal：包括 Surface heat flux（表面热通量）、Body heat flux（体热通量）、Concentrated heat flux（集中热通量），如图 2-42（b）所示。

✧ Acoustic：可设置 Inward volume acceleration（声媒介边界上点或节点的容积加速度），如图 2-42（c）所示。

✧ Fluid：包括 Concentrated pore fluid（点或节点上的集中孔隙流速）、Surface pore fluid（垂直于表面的孔隙流速），如图 2-42（d）所示。

✧ Electrical：包括压电分析中的 Concentrated charge（集中电荷）、Surface charge（面上的电荷密度）、Body charge（体上的电荷密度），如图 2-42（e）所示，热—电耦合分析中的 Surface current（面上的电流密度）、Concentrated current（集中电流）、Body current（体上的电流密度），如图 2-42（f）所示。其他的加载方式请读者参阅系统帮助文件《ABAQUS/CAE User's Manual》。

1．定义 Concentrated force（集中力）

如图 2-42（a）所示，选择 Concentrated force 之后，单击 Continue…按钮，选择施加集中力的几何实体上的参考点、顶点或网格实体上的节点，单击提示区的 Done 按钮，弹出 Edit Load 对话框，如图 2-43 所示。该对话框包括以下几项。


![image](https://user-images.githubusercontent.com/43568675/193416212-cee5dcaa-11c1-4119-bd44-379674ce8650.png)

（1）CSYS：用于选择载荷对应的坐标系，默认为整体坐标系（Global）。单击 Edit…按钮，选择局部坐标系。

（2）CF1、CF2、CF3：分别为力在三个方向上的分量。与坐标轴正方向同向的力为正值，反之为负，不输入值则默认为 0。

（3）Follow nodal rotation：用于选择集中力是否随着节点的旋转而改变。在小变形分析中可以不作选择，认为力的方向不随模型变形方向的改变而改变；而在大变形分析中应该选择该项。

（4）Amplitude（幅值）：用于选择载荷随时间/频率变化的规律。

✧ 对于静力学问题，默认的是 Ramp，如图 2-43（a）所示，为由 0 线性增长到给定值。

✧ 对于动力学问题，默认的是 Instantaneous，如图 2-43（b）所示，为瞬时加载。

若已通过 Tools→Amplitude→Create 命令定义了幅值，可以在该列表内进行选择。

若没有定义幅值，可以单击 Create…按钮定义随时间变化的加载方式，如 Equally spaced（按等时间/频率间距变化的载荷）、Tabular（由表格给定的载荷与时间/频率的关系）和 Periodic（周期变化的载荷）等。

输入集中力对应的坐标系三个方向上的分量的值或设置随时间变化的载荷后，单击 OK 按钮，完成集中力的施加。加载在几何顶点或参考点上的集中力会自动转换为加载在相应节点上的集中力。

2．定义 Moment（力矩）

如图 2-42（a）所示，在选择 Moment 之后，单击 Continue…按钮，选择施加力矩的几何实体上的参考点、顶点或网格实体上的节点，单击 Done 按钮，弹出 Edit Load 对话框，如图 2-44 所示。该对话框包括以下几项。

![image](https://user-images.githubusercontent.com/43568675/193416226-93ceed18-0d3a-48d6-81fc-603c30b3bb03.png)


（1）CSYS（坐标系）：用于选择载荷对应的坐标系，与施加集中力时的设置方法相同。

（2）CM1、CM2、CM3：分别为绕三个坐标轴的力矩，力矩的正负遵守右手法则。

（3）Amplitude（幅值）：用于选择载荷随时间/频率变化的规律，与施加集中力时的设置方法相同。

（4）Follow nodal rotation：用于选择集中力是否随着节点的旋转而改变，与施加集中力时相同。

3．定义 Pressure（单位面积上的压力）

如图 2-42（a）所示，在选择 Pressure 之后，单击 Continue…按钮，选择施加压力的几何实体的表面，载荷的方向与选择的面垂直，单击提示区的 Done 按钮，弹出 Edit Load 对话框，如图 2-45 所示。

![image](https://user-images.githubusercontent.com/43568675/193416308-a6d968fa-5841-40bc-aef4-bcdc54b4526a.png)


首先需要在 Distribution（分布）列表中选择压力的分布方式，每种分布方式都有各自的设置选项，分别介绍如下。

（1）Uniform，施加均匀分布的压力，如图 2-45（a）所示。

✧ Magnitude：输入压力值，正值为压力，负值为拉力。

✧ Amplitude：该列表用于选择载荷随时间/频率变化的规律，与施加集中力时的设置方法相同，不再赘述。

（2）Hydrostatic，施加静水压力，如图 2-45（b）所示，仅适用于 ABAQUS/Standard。

✧ Magnitude：输入压力值。

✧ Amplitude：用于选择载荷随时间/频率变化的规律。

✧ Zero pressure height：用于输入零压力处的高度。

提示

对于三维模型以 Z 轴方向（坐标轴 3 方向）为静水压力随高度变化方向；二维模型以 Y 轴方向（坐标轴 2 方向）为静水压力随高度变化方向。

✧ Reference pressure height：用于输入参考压力值（Magnitude 栏内设定的压力值）的高度。对于三维模型以Z轴方向（坐标轴 3 方向）为静水压力随高度变化方向；二维模型以Y轴方向（坐标轴 2 方向）为静水压力随高度变化方向。

（3）User-defined，使用用户子程序 DLOAD（ABAQUS/Standard）或 VDLOAD（ABAQUS/Explicit）定义压力，如图 2-45（c）所示。

✧ Magnitude：如果需要可以在该栏输入压力值。在 ABAQUS/Standard 分析中，该值被输入用户子程序 DLOAD；在 ABAQUS/Explicit 分析中，该值被忽略。

（4）Stagnation，施加滞止压力，如图 2-45（d）所示，仅适用于 ABAQUS/Explicit。

✧ Magnitude：输入压力值。

✧ Amplitude：用于选择载荷随时间/频率变化的规律。

✧ Determine relative velocity from reference point：该选项用于选择是否将施加压力的面的速度减去参考点的速度。默认为不选择该选项；若用户选择该选项，需要单击 Edit...按钮选择几何模型的顶点、参考点或网格模型的节点作为参考点。

（5）Viscous，施加黏性压力，如图 2-45（e）所示，仅适用于 ABAQUS/Explicit，其设置方法同滞止压力。

（6）Create，该按钮用于创建分析场的表达式，创建后该分析场被列入 Distribution 列表中，可选择压力按此表达式分布。

如果事先通过 Tools→Analytical Field→Create 命令定义了分析场，可以直接在 Distribution 列表内进行选择。

完成载荷的设置后，单击工具区的 Load Manager（载荷管理器）工具，可见载荷管理器内列出了已创建的载荷，如图 2-46 所示。该管理器的用法不再赘述。

![image](https://user-images.githubusercontent.com/43568675/193416352-34a0a5ac-f9d7-4828-ac24-dd5ef2ef1b4e.png)


## Day 58 载荷模块（Load）2

- [x]  定义边界条件

主菜单中的 BC 菜单及工具区中 Create Boundary Condition（创建边界条件）工具和 Boundary Condition Manager（边界条件管理器）工具用于边界条件的创建和管理。

定义边界条件时，或执行 BC→Create 命令，单击工具区中的，也可双击左侧模型树中的 BCs，弹出 Create Boundary Condition 对话框，如图 2-47 所示。该对话框与 Create Load 对话框类似，包括以下几个部分。

![image](https://user-images.githubusercontent.com/43568675/193416485-219669b4-0003-4152-8001-e3595a6e77ee.png)

（1）Name（名称），在该栏内输入边界条件的名称，默认为 BC-n（n 为第n个创建的边界条件）。

（2）Step（分析步），在该列表内选择用于创建边界条件的步骤，包括初始步和分析步。

（3）Category（种类），用于选择适用于所选步骤的边界条件种类，包括 Mechanical（力学的）和 Other（其他）。

（4）Types for Selected Step，用于选择边界条件的类型，是 Category 的下一级选项。对于不同的分析步，可以施加不同的边界条件类型。

✧ Mechanical：包括 Symmetry/Antisymmetry/Encastre（对称/反对称/端部固定）、Displacement/Rotation（位移/旋转）、Acceleration/Angular acceleration（加速度/角加速度）、Velocity/Angular velocity（速度/角速度）、Connector displacement（连接器位移）、Connector velocity（连接器速度）、Connector acceleration（连接器加速度），如图 2-47（a）所示。

✧ Other：包括 Temperature（温度）、Electric potential（电势）、Pore pressure（孔隙压力）、Mass concentration（质量浓度）、Acoustic pressure（声压），如图 2-47（b）所示。

下面对较常用的 Symmetry/Antisymmetry/Encastre 和 Displacement/Rotation 边界条件的定义做详细介绍，其他的请参阅系统帮助文件《ABAQUS/CAE User's Manual》。

1．定义 Symmetry/Antisymmetry/Encastre（对称/反对称/端部固定边界条件）

如图 2-47（a）所示，选择 Symmetry/Antisymmetry/Encastre 后，单击 Continue...按钮，选择施加该边界条件的点、线、面、cells，单击提示区的 Done 按钮，弹出 Edit Boundary Condition 对话框，如图 2-48 所示。该对话框包括以下 8 种单选的边界条件。

![image](https://user-images.githubusercontent.com/43568675/193416511-aae4c7aa-382a-4bb8-825a-5341d75922e6.png)


✧ XSYMM：关于与X轴（坐标轴 1）垂直的平面对称（Ul=UR2=UR3=0）。

✧ YSYMM：关于与Y轴（坐标轴 2）垂直的平面对称（U2=URl=UR3=0）。

✧ ZSYMM：关于与Z轴（坐标轴 3）垂直的平面对称（U3=URl=UR2=0）。

✧ PINNED：约束 3 个平移自由度，即铰支约束（Ul=U2=U3=0）。

✧ ENCASTRE：约束 6 个自由度，即固支约束（Ul=U2=U3=URI=UR2=UR3=0）。

✧ XASYMM：关于与X轴（坐标轴 1）垂直的平面反对称（U2=U3 = URI=0），仅适用于 ABAQUS/Standard。

✧ YASYMM：关于与Y轴（坐标轴 2）垂直的平面反对称（Ul=U3=UR2=0），仅适用于 ABAQUS/Standard。

✧ ZASYMM：关于与Z轴（坐标轴 3）垂直的平面反对称（Ul=U2=UR3=0），仅适用于 ABAQUS/Standard。

注意

对于结构、载荷和边界条件对称的情况（包括正对称或反对称），可以建立对称面一侧的模型用来计算，并对该对称面施加正对称或反对称边界条件。如对称面与坐标轴 l 垂直的正对称结构，选择 XSYMM。

2．定义 Displacement/Rotation（位移/旋转边界条件）

如图 2-47（a）所示，选择 Displacement/Rotation 后，单击 Continue…按钮，选择施加该边界条件的点、线、面，单击提示区的 Done 按钮，弹出 Edit Boundary Condition 对话框，如图 2-49 所示。该对话框包括如下选项。

![image](https://user-images.githubusercontent.com/43568675/193416527-c83b2fec-1a61-4aad-b2bd-9efc9b1caff3.png)


（1）CSYS，用于选择坐标系，默认为整体坐标系。单击 Edit…按钮，可以选择局部坐标系。

（2）Method，用于选择施加边界条件的方式。对于施加边界条件的分析步，只有当两种方式都有效时，该下拉列表才出现。

✧ Specify Constraints：为指定的自由度设置位移或转角。

✧ Fixed at Current Position：固定指定的自由度。若选择该选项，该对话框如图 2-49（b）所示。

（3）Distribution，用于选择边界条件的分布方式。

提示

当选择 Fixed at Current Position 方式或在 ABAQUS/Explicit 分析步中定义边界条件时，该选项不被激活。

✧ Uniform：该选项用于定义均匀分布的边界条件。

✧ User-defined：使用用户子程序 DISP 定义边界条件。

（4）Ul、U2、U3 用于指定三个方向的位移边界条件，UR1、UR2、UR3 用于指定三个方向的旋转边界条件（指定转角值为弧度）。

以上所有选项用于设置位移约束，可选择一个或多个自由度，选择之后默认为 0。如图 2-49（a）所示，表示坐标轴 1 方向的位移为 0，坐标轴 2 方向的指定位移为 l，其他方向不约束。

（5）Amplitude（幅值），用于选择边界条件随时间/频率变化的规律，与施加集中力时的设置方法相同，不再赘述。该列表仅在 Method 中选择 Specify Constraints 并在 Distribution 中选择 Uniform 时被激活，如图 2-49（a）所示。

完成边界条件的设置后，单击工具区的 Boundary Condition Manager（边界条件管理器）工具，可见边界条件管理器内列出了已创建的边界条件。该管理器的用法与 Load Manager（载荷管理器）相同，不再赘述。



## Day 60 载荷模块（Load）3

2.5.3 设置预定义场
主菜单中的 Predefined Field 菜单及工具区的 Create Predefined Field（创建预定义场）工具和 Predefined Field Manager（预定义场管理器）工具，用于预定义场的创建和管理。

执行 Predefined Field→Create 命令，或定义预定义场时，单击工具区中的工具，也可双击左侧模型树中的 Predefined Field，弹出 Create Predefined Field 对话框，如图 2-50 所示。该对话框与 Create Load 对话框类似，包括以下几项。


图 2-50 创建预定义场

（1）Name（名称），在该栏内输入预定义场的名称，默认为 Predefined Field-n（n 表示第 n 个创建的预定义场）。

（2）Step（分析步），在该下拉列表内选择用于创建预定义场的步骤，包括初始步和分析步。

（3）Category（种类），该选项用于选择适用于所选步骤的预定义场的种类，包括 Mechanical（力学的）和 Other（其他）。

（4）Types for Selected Step，该列表用于选择预定义场的类型，是 Category 的下一级选项。

① Mechanical，在初始步中设置 Velocity（速度），如图 2-50（a）所示。单击 Continue...按钮，选择施加该边界条件的点、线、面、cells，单击提示区的 Done 按钮，弹出 Edit Predefined Field 对话框，如图 2-51 所示。该对话框包括以下几项。


图 2-51 编辑初始位移场

●Definition，用于选择初始速度的定义方式。

✧ Translational only：用于定义初始平移速度。

✧ Rotational only：用于定义初始旋转速度。

✧ Translational&rotational：用于定义初始平移速度和初始旋转速度。

● V1，该栏用于输入坐标轴 1 方向（整体坐标系X轴）的平移速度。当在 Definition 中选择 Rotational only 时，该选项不被激活。

● V2，该栏用于输入坐标轴 2 方向（整体坐标系Y轴）的平移速度。当在 Definition 中选择 Rotational only 时，该选项不被激活。

● V3，该栏用于输入坐标轴 3 方向（整体坐标系Z轴）的平移速度。当在 Definition 中选择 Rotational only 时，该选项不被激活。

● Axis point l/Axis point 2，该栏用于输入旋转轴第 1/2 点的坐标。当在 Definition 中选择 Translational only 时，该选项不被激活。对于二维模型，在 Axis point 栏内输入指定点的坐标，为该点绕Z轴正方向的旋转；对于轴对称模型，在 Axis radius 栏内输入半径，为绕 Z 轴正方向以该指定半径旋转。

●Angular velocity，该栏用于输入角速度。当在 Definition 中选择 Translational only 时，该选项不被激活。

② Other，包括 Temperature（温度）和 Initial State（初始状态），如图 2-50（b）所示，其中 Initial State（初始状态）仅适用于初始步，输入以前的分析得到的已发生变形的网格和相关的材料状态作为初始状态场。

提示

若想了解 Temperature 和 Initial State 的设置，请参阅系统帮助文件《ABAQUS/CAE User's Manual》。

完成预定义场的设置后，单击工具区的 Predefined Field Manager（预定义场管理器）工具，可见预定义场管理器内列出了已创建的预定义场。该管理器的用法与载荷管理器、边界条件管理器类似。

2.5.4 定义工况
主菜单中的 Load Case 菜单及工具区中第四行的 Create Load Case（创建工况）工具和 Load Case Manager（工况管理器）工具，用于工况的创建和管理。

工况是一系列组合在一起的载荷和边界条件（可以指定非零的比例系数对载荷和边界条件进行缩放），线性叠加结构对它们的响应，仅适用于直接求解的稳态动力学线性摄动分析步（Steady-state dynamic, Direct）和静态线性摄动分析步（Static, Linear perturbation），包含工况的分析步仅支持场变量输出。

定义工况时，执行 Load Case→Create 命令，或单击工具区中的工具，弹出 Create Load Case 对话框，如图 2-52 所示。该对话框包括以下几项。


图 2-52 定义工况

✧ Name（名称）：在该栏内输入工况名称，默认为 LoadCase-n（n 为第n个创建的工况）。

✧ Step（分析步）：在该列表内选择用于创建工况的分析步。

单击 Continue…按钮，弹出 Edit Load Case 对话框，如图 2-53 所示。该对话框包括以下几项。


图 2-53 编辑工况

（1）Loads（载荷）：用于选择该工况下的载荷。可以在表格内输入载荷名称和非零的比例系数（可以为负数），勾选 Highlight selections in viewport 对选择的载荷进行高亮度显示；也可以单击 Add…按钮，在 Load Selection 对话框中进行载荷的选择。单击 Delete Rows 按钮删除已添加的载荷。

（2）Boundary Conditions（边界条件）：用于选择该工况下的边界条件。边界条件的设置与载荷的设置相同。默认选择的 In addition to selections bellow，use all boundary conditions propagated or modified from the base state 表示除了表中选择的边界条件外，该工况还包含所有传播到该分析步的边界条件（在该分析步下显示 propagated 或 modified）。

完成工况的设置后，单击工具区 Load Case Manager（工况管理器）工具，可见工况管理器内列出了该分析步内已创建的工况。


