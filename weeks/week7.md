## Day 40 Automatic（自动网格划分）

- [x] Automatic（自动网格划分）
1. 划分方式
* Automatic（自动网格划分）操作，对实体模型无特殊要求。
* 任何几何模型，尽管是不规则的，也可以进行自动网格划分。
* 所用单元形状依赖于是对面还是对体进行网格划分，对面时，自由网格可以是四边形，也可以是三角形，或两者混合；
* 对体时，自由网格一般是四面体单元，棱锥单元作为过渡单元也可以加入到四面体网格中，图 8-15 所示为采用 Automatic（自动网格划分）得出的网格分布。

<img width="399" alt="image" src="https://user-images.githubusercontent.com/43568675/190192799-1d769c2a-2923-4ec3-9aeb-9488cbba2d22.png">

2. 进行 Automatic（自动网格划分）操作的具体步骤为：
* 右击 Mesh→Insert（插入）→Method（方式），如图 8-16 所示，打开 Automatic（自动网格划分）设置明细窗口，如图 8-17 所示。

<img width="591" alt="image" src="https://user-images.githubusercontent.com/43568675/190193616-772a05a3-0f02-4fc6-941b-0672e60c9bce.png">

<img width="594" alt="image" src="https://user-images.githubusercontent.com/43568675/190193925-401c02c1-1618-4433-b07e-ba922eb07a86.png">

* Details of「Automatic Method」–Method 明细窗口中需要设置的网格划分参数如下。

· Scope（作用域）：包括 Scoping Method（作用域方式）和 Geometry（几何模型）。
其中 Scoping Method（作用域方式）包含 Geometry Selection（几何选择）和 Named Selection（命名选择），默认选择为 Geometry Selection（几何选择）。
Scope 下的 Geometry（几何模型）用来选择所要划分网格的几何模型。

· Definition（定义）：包括 Suppressed（抑制）、Method（方式）和 Element Midside Nodes（单元中间节点）。
其中 Suppressed（抑制）有 Yes 和 No 两个选项，默认选择为 No。
这里 Method（方式）选择 Automatic（自动网格划分）。
Element Midside Nodes（单元中间节点）包括 Use Global Setting（使用选项设置）、Dropped（去掉中间节点）和 Kept（保留中间节点）。

## Day 41 Tetrahedrons（四面体网格划分）

- [x] 特点
1. 对于任意几何体都可以使用，可以快速、自动生成，并适用于复杂几何，在关键区域容易使用曲度和近似尺寸功能自动细化网格，可使用膨胀细化实体边界附近的网格（边界层识别）。
2. 在近似网格密度情况下，单元和节点数高于六面体网格，一般不可能使网格在一个方向排列，由于几何和单元性能的非均质性，不适合于薄实体或环形体。

- [x] 划分方式
1. 有两种划分网格的方式，Patch Conforming 四面体和 Patch Independent 四面体，图 8-18 所示为分别采用两种方式所得到的网格。
<img width="608" alt="image" src="https://user-images.githubusercontent.com/43568675/190197774-23057acd-789d-4c2b-bc99-912c9082406b.png">
* Patch Conforming 四面体首先由默认的考虑几何所有面和边的 Delaunay 或 Advancing Front 表面网格划分器生成表面网格（注意：一些内在缺陷在最小尺寸限度之下），然后基于 TGRID Tetra 算法由表面网格生成体网格。
Patch Conforming 四面体方法考虑面和它们的边界（边和顶点），包含膨胀因子的设定，控制四面体边界尺寸的内部增长率，CFD 的膨胀层或边界层识别。不同部分有不同的方法，多体部件可混合使用 Patch Conforming 四面体和 Sweep（扫掠）方法生成共形网格。Patch Conforming 方法可以联合 Pinch Controls 功能，有助于移除短边。

进行 Patch Conforming 操作的具体步骤为：右击 Mesh→Insert（插入）→Method（方式），将 Method 设置为 Tetrahedrons，Algorithm 设置为 Patch Conforming 打开 Patch Conforming 设置明细窗口，如图 8-19 所示。
<img width="609" alt="image" src="https://user-images.githubusercontent.com/43568675/190198996-eb6d45ec-256a-4e96-b26d-f4cd6c7c998c.png">

Details of「Patch Conforming Method」–Method 明细窗口中的 Scope（作用域）和 Definition（定义）与前面 Automatic（自动网格划分）一样，这里不再赘述。

*  Patch Independent 四面体生成体网格并映射到表面产生表面网格。如没有载荷，边界条件或其他作用，面和它们的边界（边和顶点）不必要考虑。这个方法更加容许质量差的 CAD 几何，Patch Independent 算法基于 ICEM CFD Tetra 算法。

进行 Patch Independent 操作的具体步骤为：右击 Mesh→Insert（插入）→Method（方式），将 Method 设置为 Tetrahedrons，Algorithm 设置为 Patch Independent，打开 Patch Independent 设置明细窗口，如图 8-20 所示。Patch Independent 操作的 Scope（作用域）和 Definition（定义）与 Patch Conforming 操作的 Scope（作用域）和 Definition（定义）作用一样，这里不再重复。我们主要看一下 Advanced（高级选项）。

<img width="602" alt="image" src="https://user-images.githubusercontent.com/43568675/190199954-f8b224e4-13ee-4255-b0d7-50bd5313d380.png">

Advanced（高级选项）：包括 Defined By（定义）、Mesh Based Defeaturing（基于几何损伤的网格）、Curvature and Proximity Refinement（曲率和邻近细化）、Smooth Transition（平滑度）、Growth Rate（增长比例）、Minimum Edge Length（最小线段长度）和 Write ICEM CFD Files（写入 ICEM CFD 文件）。

其中 Defined By（定义）包括 Max Element Size（最大单元尺寸）和 Approx number of Elements（单元近似数量）。Max Element Size（最大单元尺寸）一般系统会提供默认值，用户可根据自己问题的实际情况，设置 Max Element Size（最大单元尺寸）。Feature Angle（特征角）的默认值为 30°，系统提供了 0°～90° 的变化范围。

Mesh Based Defeaturing（基于几何损伤的网格）系统默认为 Off，当选择 ON 时，将弹出图 8-21 所示的 Defeaturing Tolerance（损伤容差），系统提供一个默认值，用户可以根据工程需要自己设定损伤容差值来调整损伤网格，以满足工程需求。

Curvature and Proximity Refinement（曲率和邻近细化）系统默认为 Yes，包括 Min Size Limit（最小尺寸限制），Num Cells Across Gap（狭缝地带所希望的网格层数）和 Curvature Normal Angle（曲率法角），系统提供一个默认值，用户可以根据工程需要自己设定这些参数，以满足工程需求。

Smooth Transition（平滑度）系统默认为 Off，当选择 ON 时，系统将提供一个默认值，用户可以根据工程实际进行调整。Growth Rate（增长比例）系统默认为 0，最大可设置为 5。Minimum Edge Length（最小线段长度）系统也提供了一个默认值供参考，用户也可以根据工程实际进行调整设置。

Write ICEM CFD Files（写入 ICEM CFD 文件）系统默认选项为 NO，用户还可根据工程的实际需要进行其他选择，这里提供了其他 3 种选项，包括 Yes、Interactive（交互作用）和 Batch（批处理）。当选择 Interactive（交互作用）时，将弹出如图 8-22 所示的 ICEM CFD Behavior 选项。ICEM CFD Behavior 提供了两个选项，Post Operation（后操作）和 Override Method（覆盖方式）。当选择 Batch（批处理）选项时，也将出现 Post Operation（后操作）和 Override Method（覆盖方式）两个选项。

## Day 42  Hex Dominant（六面体主导网格法）

- [x] 划分方式
Hex Dominant（六面体主导网格）法则先生成四边形主导的面网格，再得到六面体，再按需要填充棱锥和四面体单元。

- [x] 适用
此方法对于不可扫掠的体，要得到六面体网格时被推荐，对内部容积大的体有用，对体积和表面积比较小的薄复杂体无用，对于 CFD 无边界层识别，主要对 FEA 分析有用。

- [x] 操作步骤
进行 Hex Dominant（六面体主导网格）操作的具体步骤为：右击 Mesh→Insert（插入）→Method（方式），在 Method（方式）右侧选择 Hex Dominant（六面体主导网格），打开 Hex Dominant（六面体主导网格）设置明细窗口。
<img width="596" alt="image" src="https://user-images.githubusercontent.com/43568675/190551183-da048c20-e307-487d-8934-d0239058fb3d.png">

Details of「Hex Dominant Method」–Method 明细窗口中的 Scope（作用域）与前面 Automatic（自动网格划分）一样，这里不再赘述。

- [x] 操作选项
Definition（定义）：包括 Suppressed（抑制）、Method（方式）、Element Midside Nodes （单元中间节点）、Free Face Mesh Type（自由面网格类型）和 Control Messages（控制信息）。其中 Suppressed（抑制）、Method（方式）、Element Midside Nodes（单元中间节点）与前面 Automatic（自动网格划分）一样。这里主要介绍一下 Free Face Mesh Type（自由面网格类型）。系统提供了两种网格，分别为 Quad/Tri（四边形/三角形）和 All Quad（全四边形），图 所示为选择两种不同网格时的效果图。Control Messages（控制信息）系统默认为 NO。
<img width="604" alt="image" src="https://user-images.githubusercontent.com/43568675/190551765-6b7063f9-63bc-49c6-9d7c-80666c3d60c4.png">

## Day 43 Sweep（扫掠法）

- [x] 拓扑模型判定
采用 Sweep（扫掠）法划分网格，首先应该确定体的拓扑模型是否能够进行扫掠，如果是下列情况之一，则不能扫掠：
1. 体的一个或多个侧面包含多于一个环；体包含多于一个壳；体的拓扑源面与目标面不是相对的。
2. 其次应该确定已定义合适的二维和三维单元类型，例如，如果对源面进行预网格划分，并想扫掠成包含二次六面体的单元，应当先用二次二维面单元对源面划分网格。
接下来需要确定在扫掠操作中如何控制生成单元层数，即沿扫掠方向生成的单元数。
然后确定体的源面和目标面。ANSYS 在源面上使用的是面单元模式（三角形或者四边形），用六面体或者楔形单元填充体。目标面是仅与源面相对的面。最后有选择地对源面、目标面和边界面划分网格。

- [x] 操作步骤
进行 Sweep（扫掠法）操作的具体步骤为：右击 Mesh→Insert（插入）→Method（方式），在 Method（方式）右侧选择 Sweep（扫掠法），打开 Sweep（扫掠法）设置明细窗口，如图所示。

<img width="592" alt="image" src="https://user-images.githubusercontent.com/43568675/190561849-ebaf41f4-28ad-4a83-af74-117dee4441ed.png">
Details of「Sweep Method」–Method 明细窗口中的 Scope（作用域）与前面 Automatic（自动网格划分）一样，这里不再赘述。


- [x] 操作选项

Definition（定义）：包括 Suppressed（抑制）、Method（方式）、Element Midside Nodes（单元中间节点）、Src/Trg Selection（Src/Trg 选项）、Free Face Mesh Type（自由面网格类型）、Type（类型）、Sweep Bias Type（扫掠偏差类型）和 Element Option（单元选项）。

其中 Suppressed（抑制）、Method（方式）、Element Midside Nodes（单元中间节点）与前面 Automatic（自动网格划分）一样。这里主要介绍以下几个选项。

·Src/Trg Selection（Src/Trg 选项）包括 5 个选项，分别是 Automatic、ManualSource、Manual Source and Target、Automatic Thin 和 Manual Thin。当选择 Automatic 时，Source 和 Target 系统都默认为 Program Controlled，用户不需要自己进行选择，如图所示。

<img width="478" alt="image" src="https://user-images.githubusercontent.com/43568675/190562078-47b5f584-9adf-4c09-986e-299e722a777f.png">


当选择 Manual Source 和 Manual Thin 时，均需要用户自己选择 Source，如图 所示，区别在于前者的 Target 系统默认为 Program Controlled，而后者只考虑 Source，而未考虑 Target。

<img width="614" alt="image" src="https://user-images.githubusercontent.com/43568675/190562121-d1e6d08c-dcf3-4fb7-97c5-fe699e2790ef.png">



当选择 Manual Source and Target 时，用户需要自己选择 Source 和 Target，如图 所示。当选择 Automatic Thin 时，系统默认 Source 为 Program Controlled，用户不需要自己进行选择，如图所示。
<img width="536" alt="image" src="https://user-images.githubusercontent.com/43568675/190563138-074eee4d-0f00-42ac-81c3-e5371e2d4c21.png">

<img width="470" alt="image" src="https://user-images.githubusercontent.com/43568675/190562234-f9894460-ace1-428f-bac8-0bc73ae5305a.png">




·Free Face Mesh Type（自由面网格类型）包括 3 个选项，分别为 All Tri（全三角形）、Quad/Tri（四边形/三角形）和 All Quad（全四边形）。图所示为分别选择 All Tri（全三角形）和 Quad/Tri（四边形/三角形）时划分的网格。
<img width="478" alt="image" src="https://user-images.githubusercontent.com/43568675/190562896-c4050bb0-515c-4a2b-9d06-3f9622d6ee01.png">

<img width="622" alt="image" src="https://user-images.githubusercontent.com/43568675/190562303-a35bd50d-f712-4579-ae52-200578663781.png">


·Type（单元）包括两个选项，分别是 Element Size 和 Number of Divisions，系统默认为 Number of Divisions。当选择 Number of Divisions 时，如图  所示，我们从图中可以看到 Sweep Num Divs 系统默认值为 0，可以根据工程实际自己进行调整。当我们把 Sweep Num Divs 数值设置为 2 和 4 时，可以得到图  所示的网格。

<img width="592" alt="image" src="https://user-images.githubusercontent.com/43568675/190563103-11937152-dcd2-4a96-a0cc-08dfbb17e1bc.png">




·Sweep Bias Type（扫掠偏差类型）包括 5 个选项，系统默认为 NO Bias。当选择其他 4 个选项时，将会出现 Sweep Bias 选项，默认为 0。如图 8-33 所示，当我们依次选择 4 种类型，设置 Sweep Bias 为 20 时，得到不同的网格效果。

## Day 44 MultiZone（多区法）

- [x] 特点
MultiZone（多区网格划分）的特征是自动分解几何，从而避免将一个体分裂成可扫掠体以用扫掠方法得到六面体网格。MultiZone（多区网格划分）不利用高级尺寸功能（只用 Patch Conforming 四面体和扫掠方法）。MultiZone（多区网格划分）的源面选择不是必须的，但是是有用的，可以拒绝或允许自由网格程序块。

- [x] 操作步骤
进行 MultiZone（多区网格划分）的具体步骤为：右击 Mesh→Insert（插入）→Method （方式），在 Method（方式）右侧选择 MultiZone（多区网格划分），打开 MultiZone（多区网格划分）设置明细窗口，如图所示。

![image](https://user-images.githubusercontent.com/43568675/190862030-a69b456c-002e-488e-837f-56fa488bcaea.png)

Details of「MultiZone Method」–Method 明细窗口中的 Scope（作用域）与前面 Automatic（自动网格划分）一样，这里不再赘述。


- [x] 操作选项

Definition（定义）：包括 Suppressed（抑制）、Method（方式）、Mapped Mesh Type（映射网格类型）、Surface Mesh Type（表面网格类型）、Free Mesh Type（自由网格类型）、Element Midside Nodes（单元中间节点）和 Src/Trg Selection（Src/Trg 选项）。其中 Suppressed（抑制）、Method（方式）、Element Midside Nodes（单元中间节点）、Src/Trg Selection（Src/Trg 选项）与前面 Automatic（自动网格划分）一样。其中 Mapped Mesh Type（映射网格类型）包括 Hexa（六面体）、Hexa/Prism（六面体/棱柱）和 Prism（棱柱）3 种。

![image](https://user-images.githubusercontent.com/43568675/190862077-7a4e40ac-8d02-4a7f-947d-34c90bede332.png)


Surface Mesh Type（表面网格类型）包括 Program Controlled、Uniform 和 Pave 3 种类型。图 8-36 所示为不同表面网格类型产生的网格。

![image](https://user-images.githubusercontent.com/43568675/190862094-8c6c083f-5d53-4fd1-9d70-83a25f2bfa0d.png)

Free Mesh Type（自由网格类型）包括 Not Allowed（不允许）、Tetra（四面体）、Hexa Dominant（六面体-支配）和 Hexa Core（六面体-核心）。

Advanced（高级选项）：Mesh Based Defeaturing（基于几何损伤的网格）、Minimum Edge Length（最小线段长度）和 Write ICEM CFD Files（写入 ICEM CFD 文件）。前面章节已有详细介绍，这里不再赘述。

## Day 45 Inflation（膨胀法）

- [x] 操作步骤
进行 Inflation（膨胀法）的具体步骤为：单击 Mesh 选项，弹出 Details of Mesh 面板，在 Details of Mesh 下选择 Inflation（膨胀法）选项，打开 Inflation（膨胀法）设置明细窗口，如图。

![image](https://user-images.githubusercontent.com/43568675/190899433-59e78315-4a48-4482-8395-ed520aa5dfc9.png)

Inflation（膨胀法）包括 Use Automatic Inflation（使用自动控制膨胀层）、Inflation Option（膨胀层选项）、Inflation Algorithm（膨胀层算法）和 View Advanced Options（显示高级选项）。

1. Use Automatic Inflation（使用自动控制膨胀层）包括 3 个选项，
* None（不使用自动控制膨胀层）  系统默认的选项
* Program Controlled（程序控制膨胀层）
* All Faces in Chosen Named Selection（以命名选择所有面）



2. Inflation Option（膨胀层选项）包括 5 个选项，
* Total Thickness（总厚度）        
当选择 Total Thickness（总厚度）时（见图 8-38），Number of Layers（膨胀层层数）系统默认为 5，最小为 1；Growth Rate（增长速率）系统默认为 1.2；Maximum Thickness（最大厚度）需要用户自定义。这几个参数用户均可根据工程实际进行调整。
![image](https://user-images.githubusercontent.com/43568675/190899620-21fe1b65-ef23-46a6-b92c-08647ecb3027.png)



* First Layer Thickness（第一层厚度）
当选择 First Layer Thickness（第一层厚度）时（见图 8-39），First Layer Height（第一层高度）需要用户自定义；Maximum Layers（最大边膨胀层层数），系统默认为 5，最小为 1；Growth Rate（增长速率）系统默认为 1.2。
![image](https://user-images.githubusercontent.com/43568675/190899672-9a206f5f-cb15-486d-a613-64d16e5b42bc.png)




* Smooth Transition（平滑过渡）
当选择 Smooth Transition（平滑过渡）时（见图 8-40），Transition Ratio（平滑比率）系统默认为 0.272，Maximum Layers（最大边膨胀层层数）和 Growth Rate（增长速率）同上。
![image](https://user-images.githubusercontent.com/43568675/190899683-57b13b0d-3fc0-4075-8ee4-448aa15fdf88.png)



* First Aspect Ratio（第一个网格的宽高比）
当选择 First Aspect Ratio（第一个网格的宽高比）时（见图 8-41），First Aspect Ratio（第一个网格的宽高比）系统默认为 5，Maximum Layers（最大边膨胀层层数）和 Growth Rate（增长速率）同上。
![image](https://user-images.githubusercontent.com/43568675/190899708-ee549682-a86b-42f0-b8d0-e8c4791073b8.png)



*  Last Aspect Ratio（最后一个网格的宽高比）
当选择 Last Aspect Ratio（最后一个网格的宽高比）时（见图 8-42），First Layer Height（第一层高度）需要用户自定义；Maximum Layers（最大边膨胀层层数）同上；Aspect Ratio（Base/Height）（宽高比）系统默认为 3。
![image](https://user-images.githubusercontent.com/43568675/190899713-a9be1aa3-1231-4e2b-ba86-55ac3522f0e3.png)



3. Inflation Algorithm（膨胀层算法）
 有 Pre（前处理）和 Post（后处理）两种。
* Pre（前处理）基于 Tgrid 算法，所有物理模型的默认设置。首先表面膨胀，然后生成体网格，可应用扫掠和二维网格的划分，但是不支持邻近面设置不同的层数。
* Post（后处理）基于 ICEM CFD 算法，使用一种在四面体网格生成后作用的后处理技术，后处理技术只对 Patching Conforming 和 Patch Independent 四面体网格有效。

4. View Advanced Options（显示高级选项）包括 Yes 和 NO 两种选项，系统默认为 NO。
当 View Advanced Options（显示高级选项）选择性 Yes 时，此时 Inflation（膨胀层）设置会增加图 8-43 所示的选项。
![image](https://user-images.githubusercontent.com/43568675/190899840-b916cab9-caed-46e7-a712-a090c7cf437a.png)
