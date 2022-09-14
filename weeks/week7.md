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
