## Day 61 ABAQUS 小结

ABAQUS 的所有功能都集成在各功能模块中，用户根据需要在 ABAQUS/CAE 主界面中激活各功能模块，对应的菜单和工具栏随即出现在界面中。

Part 模块、Sketch 模块、Assembly 模块、Property 模块、Step 功能模块和 Load 模块的功能

（1）ABAQUS 的模型是基于 CAD 软件中的部件和组装的概念建立起来的。
     ABAQUS 的模型包括一个或多个部件，所有部件都在 Part 模块中建立，部件的草图在 Sketch 模块中创建，各部件在 Assembly 模块中进行组装，Property 模块用于定义材料属性和截面特性。

（2）Step 功能模块可进行分析步和输出的定义，也可以进行求解控制和自适应网格划分的设置，这些功能包含在主菜单的 Step、Output 和 Other 中。

在 Load 功能模块施加载荷和边界条件及在 Interaction 功能模块定义接触前，需要创建分析步，选择在初始步还是分析步中设置接触和边界条件，载荷则只能设置在分析步中。

（3）Load（载荷）功能模块主要用于定义模型装配件的载荷、边界条件、预定义场和载荷状况，在进入该模块之前，用户需要在 Assembly（装配）功能模块中创建装配件并完成各部件实体的定位。

## Day 62 接触属性的定义

执行 Interaction→Property→Create 命令，或单击工具区中的 Create Interaction Property（创建相互作用属性）工具，ABAQUS 弹出 Create Interaction Property 对话框，如图 3-1 所示。该对话框包括两个部分。

<img width="339" alt="image" src="https://user-images.githubusercontent.com/43568675/194737649-c2a467a9-22fa-4661-b2e9-5038b2e075c2.png">

图 3-1 Create Interaction Property 对话框

✧ Name（名称）：该处输入相互作用属性的名称，默认为 IntProp-n（n 表示第n个创建的相互作用属性）。

✧ Type（类型）：该列表用于选择相互作用属性的类型，包括 Contact（接触）、Film condition（薄膜表面散热）、Acoustic impedance（声阻）、Incident wave（入射波）、Actuator/sensor（传动和传感特性）。

在列表中选择 Contact，单击 Continue…按钮，弹出 Edit Contact Property（编辑接触属性）对话框，如图 3-2 所示。该对话框包括 Contact Property Options 列表和各种接触参数的设置区域，下面分别进行介绍。


图 3-2 Edit Contact Property 对话框

1．Contact Property Options（接触属性选项）

用于选择接触属性的类型，选择的接触属性会依次出现在列表中。其中包括两个下拉菜单。

（1）Mechanical（力学的），用于定义力学的接触属性。

✧ Normal Behavior（法向属性）：选择定义接触刚度等法向接触属性。

✧ Tangential Behavior（切向属性）：选择定义摩擦系数、剪应力极限、弹性滑动等摩擦属性。

✧ Geometric Properties（几何属性）：选择定义附加的几何属性。

✧ Damping（阻尼）：选择定义对接触面相对运动的阻尼。

（2）Thermal（热学的），用于定义由摩擦产生的热接触属性。

✧ Heat Generation（产热）：选择定义由接触面的相互作用导致生热的能量损耗分数，适用于热—电耦合分析（Coupled thermal-electrical）或热—力耦合分析（Coupled temperature—displacement）。

✧ Thermal Conductance（热传导）：选择定义接触面间的热传导率。

✧ Radiation（热辐射）：用于定义靠近的接触面间的热辐射属性。

2．Data field（数据区）

出现在 Contact Property Options 的下方，在该区域内设置相应的接触属性值。

本节主要介绍力学分析中常用的 Normal Behavior（法向属性）和 Tangential Behavior（切向属性），其他类型的接触属性请读者参见系统帮助文件。

（1）Normal Behavior（法向属性），用于设置接触压力与穿透的关系。

① Constraint enforcement method，该栏用于选择约束增强方法。

●Default，为默认选项，采用接触压力与穿透的关系。

此时，可以通过 Pressure-Overclosure 栏选择硬接触和四种软接触，下面分别进行介绍。

✧ Hard Contact（硬接触）：在 ABAQUS/Standard 中采用拉格朗日乘子方法或在 ABAQUS/Explicit 中采用罚函数方法来加强接触约束。

提示

此时会出现一个选项 Allow separation after contact，默认为选择该选项，不选择该选项表明一旦接触后，接触面不再分离。

✧ Linear（线性的）：该选项用于指定接触压力与穿透的线性关系。读者需要在 Contact stiffness 栏输入接触刚度，即接触压力—穿透关系曲线的斜率，必须为正值。

✧ Exponential（指数的）：该选项用于指定接触压力与穿透的指数关系。读者需要在数据表中输入零间距时的接触压力值和零接触压力时的间距。其中，Maximum stiffness 栏可以设置模型的最大接触刚度，仅适用于 ABAQUS/Explicit，默认选项为 Infinite（no slip），表示在运动接触中最大接触刚度为无限大，在罚函数接触中最大接触刚度为默认罚函数刚度；若选择 Specify，则用户指定最大接触刚度。

✧ Tabular（列表）：以表格形式指定分段线性的接触压力—穿透关系，需要在数据表中输入接触压力与对应的穿透量，接触压力和穿透量必须是单调递增的，且必须以零压力开始。

提示

当穿透量大于表中的最大穿透量时，接触压力—穿透关系以用户定义的最后斜率外推。

✧ Scale Factor（General Contact）：以缩放默认接触刚度的公式指定分段线性的接触压力—穿透关系，仅适用于 ABAQUS/Explicit 中的 General Contact（通用接触），需要在 Overclosure 栏输入正值的穿透量，可以选择 measure（直接输入穿透量）和 factor（输入最小单元尺寸的分数）两种方式。

提示

还需要在 Contact stiffness scale factor 栏输入大于 l 的默认接触刚度的放大因子，当穿透超过 Overclosure 栏中指定的穿透量时，接触刚度乘以该放大因子。另外，可以选择在 Initial stiffness scale factor 栏输入初始刚度的比例因子，该比例因子必须大于 0，默认值为 1。

② Augmented Lagrange（Standard），仅适用于 ABAQUS/Standard，采用扩张的拉格朗日方法。此时仅能选择 Hard Contact（硬接触）。

✧ Contact stiffness（接触刚度）：用于指定接触刚度。默认选项为 Use default，ABAQUS 自动计算出罚函数接触刚度；可以选择 Specify，输入正值的接触刚度。

✧ Allow separation after contact：默认为选择该选项，接触后接触面可以分离。不选择该选项表明一旦接触后，接触面不再分离。

✧ Clearance at which contact pressure is zero（接触压力为零时的间距）：用于输入接触压力为零时主面和从面的间距，默认值为 0。

✧ Contact stiffness scale factor（接触刚度的比例因子）：用于输入接触刚度的比例因子，该比例因子必须大于 0，默认值为 1。

③ Penalty（Standard），采用罚函数方法，仅适用于 ABAQUS/Standard。此时，仅能选择 Hard Contact（硬接触）。面板设置与扩张的拉格朗日方法（Augmented Lagrange）相同。

（2）Tangential Behavior（切向属性），主要设置摩擦公式（Friction formulation），共有 6 个选项。

① Frictionless（无摩擦的），此为默认选项，用于定义无摩擦的接触面。

② Penalty（罚函数），用于定义罚函数摩擦公式，包含 3 个页面。

●Friction（摩擦）页面，用于定义摩擦系数。

✧ Directionality（方向性）：用于选择摩擦的方向，有两个选项：Isotropic（各向同性），仅输入一个统一的摩擦系数，为默认选项；Anisotropic（各向异性），需要设定两个正交方向的摩擦系数，仅适用于 ABAQUS/Standard。

✧ Use slip-rate-dependent data：勾选该选项表示摩擦系数与滑动速度相关，在数据表中出现 Slip Rate 栏。

✧ Use temperature-dependent data：勾选该选项表示摩擦系数与温度相关，在数据表中出现 Te mp 栏。

✧ Use contact-pressure-dependent data：勾选该选项表示摩擦系数与接触压力相关，在数据表中出现 Contact Pressure 栏。

✧ Number of field variables：该选项用于设置与摩擦系数相关的场变量的数目，在数据表中出现 Field 1、Field 2、…、Field n 栏（n 为场变量的数目），默认值为 0。

对话框下部的数据表用于设置摩擦系数及相关参数。

●Shear Stress（剪应力）页面，用于设置对剪应力的限制。

✧ No limit（不限制）：此为默认选项，在滑动前，不限制接触面的剪应力。

✧ Specify（指定）：该选项用于指定剪应力极限，当剪应力达到该极限值时，开始滑动。

● Elastic Slip（弹性滑动）页面，分别设置 ABAQUS/Standard 和 ABAQUS/Explicit 中的弹性滑动。

✧ Specify maximum elastic slip：用于设置最大弹性滑动距离，仅适用于 ABAQUS/Standard，包括两个单选项，一是 Fraction of characteristic surface dimension，此为默认选项，以特征接触面长度的最小分数作为允许的最大弹性滑动，默认值为 0.005；二是 Absolute distance，直接输入允许的最大弹性滑动距离。

✧ Elastic slip stiffness：用于设置弹性滑动刚度，仅适用于 ABAQUS/Explicit，包括两个单选项，一是 Infinite（no slip），此为默认选项，指定无弹性滑动；二是 Specify，指定剪应力与弹性滑动关系曲线的斜率。

③ Static-Kinetic Exponential Decay，用于指定静/动摩擦系数和弹性滑动，包含两个页面。

●Friction 页面，主要用于设置静摩擦系数和动摩擦系数指数衰减关系，包括两种方式。

✧ Coefficients（系数）：直接指定静摩擦系数、极限滑动速度下的动摩擦系数和衰减系数来定义静摩擦系数和动摩擦系数指数衰减关系。

✧ Test data（测试数据）：设置静摩擦系数、指定滑动速度和对应的动摩擦系数、极限滑动速度下的动摩擦系数。

●Elastic Slip（弹性滑动）页面，与罚函数摩擦公式（Penalty）的选项完全相同。

④ Rough（粗糙的），该选项用于定义无限大的摩擦系数，一旦接触，则不发生相对滑动。

⑤ Lagrange Multiplier（Standard only），使用拉格朗日乘子来加强接触面的黏性约束，仅适用于 ABAQUS/Standard。该摩擦公式包含两个页面 Friction（摩擦）和 Shear Stress（剪应力），页面设置与罚函数摩擦公式（Penalty）完全相同。

⑥ User-defined（用户子程序），该选项用于选择用户子程序 FRIC（ABAQUS/Standard）或 VFRIC（ABAQUS/Explicit）进行分析。该对话框包含两个选项。

●Number of state-dependent variables，用于指定与解答相关的状态变量的数量。

●Friction Properties，该数据表用于输入用户子程序中需要的摩擦系数。

设置完成后，单击 OK 按钮。

提示

读者可以修改接触属性，修改方法：单击工具区中的 Interaction Property Manager（相互作用属性管理器）工具，弹出如图 3-3 所示的对话框，选择需要编辑的接触属性，单击 Edit…按钮；或执行 Interaction→Property→Edit 命令后，在下级菜单中选择需要编辑的接触属性。


图 3-3 Interaction Property Manager 对话框
