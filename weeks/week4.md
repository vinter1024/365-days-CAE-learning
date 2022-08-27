## Day 18 流体有限元分析前处理知识2

> [ANSYS Fluent19.0流体有限元分析视频教程]( https://www.bilibili.com/video/BV1Dt4y1x7Ms)

- [x] Fluent19.0 启动界面

1. 选择模型纬度：2维/3维

2. 显示选项
* display mesh after reading 激活此项则导入网格后显示网格，否则不直接显示
* workbench color scheme 激活此项目采用蓝色渐变背景图像窗口，否则采用黑色背景的fluent经典图形窗口

3. 求解器选项
* double precision 为双精度求解器，不激活则采用单精度求解器

- 单精度求解器能满足大多数情况，很好的满足精度要求，且计算量小

- 双精度求解器：
 a. 几何特征包含某些极端尺度（非常长&窄的管道）
 b. 几何模型包含多个通过小直径管道相互连接的体，而且每一个区域的压力特别大（因为用户只能设定一个总体的参考压力位置），此次双精度求解器可能更能体现压差带来的流动（如渐缩渐扩管的无粘与可压缩流动模拟）
 c. 对于某些高导热系数比或高宽纵比的网格，使用单精度可能遇到收敛性不佳or 精确度不足问题
 
*  meshing mode为meshing模式，若不选择此项则采用solution模式

4. 并行设置
* serial为采用串行计算
* parallel 为并行计算设置，可以选择多核双核

5. 版本选择：多个fluent版本可以选择使用哪个版本

6. pre/post only 激活此项只利用fluent进行前后处理

7. 设置工作路径

8. 设置fluent应用程序路径

9. use journal file 激活此项记录journal脚本文件，否则不记录

- [x] Fluent19.0 工作界面
1. 软件图形用户界面
<img width="723" alt="image" src="https://user-images.githubusercontent.com/43568675/185835629-d3eab239-7300-4678-809b-1f130ab12ec9.png">

2. 软件文字用户界面

图形用户界面（GUI）文本用户界面（TUI）
* 高级命令只在TUI中可用
* 回车键展示当前级别的命令
* “q” 返回上一级命令
<img width="629" alt="image" src="https://user-images.githubusercontent.com/43568675/185837742-d827d0ca-a9bf-4bb2-aca7-3227c59ee3db.png">

3. 菜单栏
<img width="544" alt="image" src="https://user-images.githubusercontent.com/43568675/185838476-8a3014a9-ca4d-43fa-8f9e-d87307dab530.png">

4. 文件类型
* mesh文件（*. msh） fluent可识别的网格文件
* case文件（*. cas）包含网格 边界条件和解的控制参数
* data文件（*.dat）包含计算的结果数据
* journal 文件（*.jou）包含所有的操作命令

## Day 19 Fluent软件求解流程
- [x] 输入网格文件
1. file->read ->mesh
<img width="1031" alt="image" src="https://user-images.githubusercontent.com/43568675/186067691-0b1e26ed-cab9-46e7-a020-3914ed2e2f1d.png">

- [x]  网格操作

 1. 网格质量检测
<img width="616" alt="image" src="https://user-images.githubusercontent.com/43568675/186070492-b9bfda24-9d3b-45b4-9da5-e647736d6609.png">

2. 网格缩放
3. 网格平移
4. 网格旋转
<img width="554" alt="image" src="https://user-images.githubusercontent.com/43568675/186071289-589f82e4-b9a7-4194-bd74-07f7e6b6e011.png">

- [x]  选择求解器**
<img width="1021" alt="image" src="https://user-images.githubusercontent.com/43568675/186071569-ed9f669e-4f2f-4e07-b6ec-d1b0367b316c.png">

- [x]  选择物理模型**
<img width="880" alt="image" src="https://user-images.githubusercontent.com/43568675/186072082-1afd07f9-c527-45fc-8d13-f2ae9124609d.png">

<img width="951" alt="image" src="https://user-images.githubusercontent.com/43568675/186075852-432c2b6a-fa6c-461a-960f-6fb87f1e9545.png">

<img width="998" alt="image" src="https://user-images.githubusercontent.com/43568675/186078723-8df5838c-3c45-4767-a347-b687173bda8f.png">


- [x]  定义流体属性
<img width="1014" alt="image" src="https://user-images.githubusercontent.com/43568675/186078855-3258dc79-8cac-4f63-8340-649c64447ed7.png">

- [x]   定义操作条件
<img width="987" alt="image" src="https://user-images.githubusercontent.com/43568675/186078990-b2ee3dfd-c9ca-4db5-9e94-79eb69007e53.png">

- [x]  定义边界条件**
<img width="942" alt="image" src="https://user-images.githubusercontent.com/43568675/186079087-25810087-ade2-42e1-860a-148fc107fd2a.png">
<img width="802" alt="image" src="https://user-images.githubusercontent.com/43568675/186079267-96ad7cec-e234-43ee-a995-685fc37c22d2.png">

- [x]  设置参考值
<img width="854" alt="image" src="https://user-images.githubusercontent.com/43568675/186079494-0de53faa-6cb1-40ec-a3e7-04610daf7e70.png">

- [x]  求解方法以及参数**
<img width="998" alt="image" src="https://user-images.githubusercontent.com/43568675/186079606-db12c685-0814-493d-8c51-a02d4747ed81.png">


- [x]  设置收敛监视
<img width="716" alt="image" src="https://user-images.githubusercontent.com/43568675/186084478-64c8685e-b3dd-4e37-868a-1a064cbce669.png">

- [x]   定义初始条件
<img width="315" alt="image" src="https://user-images.githubusercontent.com/43568675/186087042-b73b2c8f-952f-40e8-ae51-3d4cf5cf9cb9.png">

- [x]   设置自动存储
<img width="900" alt="image" src="https://user-images.githubusercontent.com/43568675/186087154-71ca9ccb-639f-473b-b67e-3ad9c13d572f.png">

文件的压缩格式 *.gz

- [x]   迭代计算
<img width="453" alt="image" src="https://user-images.githubusercontent.com/43568675/186089113-e547464a-f642-4538-9c50-33ad47819c34.png">

- [x]   保存结果
<img width="292" alt="image" src="https://user-images.githubusercontent.com/43568675/186089578-2eab4740-cd54-4d73-bebc-6887ff823ae3.png">


## Day 20 fluent 后处理
- [x]  后处理工具
<img width="701" alt="image" src="https://user-images.githubusercontent.com/43568675/186326062-eef648cb-b054-4748-9e59-0c3e95e7c321.png">

1. 流场截面生成
<img width="77" alt="image" src="https://user-images.githubusercontent.com/43568675/186332624-9d208ef6-10d3-4de6-bd23-36344a8f8078.png">

2. 可视化后处理

【Graphic】
* mesh 网格
* contours 热力图
* vectors 矢量
* pathlines 流线
* particle tracks 粒子示踪
* hsf file

【plots】
* XY plot 曲线图
* histogram 柱状图
* residuals 残差图


3. 数据报告
把某个计算域参数

4. 动画
瞬态流场进行录制播放

5. 其他参数
具有离散项的流场，具有辐射的一些参数


- [x]  生成面
将计算域中的一部分作为surface 用于可视化和定量曲线等后处理

产生面的方式：
* zone surfaces （自动生成）
* partition surfaces
* point surfaces
* line and rake surfaces
* plane surfaces
* ISO-surfaces
* clipping surfaces

面可以重命名 删除

- [x]  可视化展示
参考 2
<img width="762" alt="image" src="https://user-images.githubusercontent.com/43568675/186334817-0437e011-9cc0-494c-b011-1272b40c6ec3.png">

<img width="765" alt="image" src="https://user-images.githubusercontent.com/43568675/186334899-c7dc0884-9e9e-4fb9-bef2-7953f14c51a3.png">

调整鼠标操作

- [x]  数据报告
1. 通量报告
* 净通量的计算
* 总的热传输率

2. 受力
3. 面积分
求解某个面平均压力
4. 体积分

<img width="760" alt="image" src="https://user-images.githubusercontent.com/43568675/186335074-6d700cc8-0e2f-4c36-8f89-f7c1e460b12f.png">

- [x]  其他后处理形式
<img width="784" alt="image" src="https://user-images.githubusercontent.com/43568675/186335435-381a5ba1-caaf-4d6f-a49d-e567eff492d1.png">

## Day 21 混合弯管二维流动和传热问题1 
<img width="882" alt="image" src="https://user-images.githubusercontent.com/43568675/186592223-df6adab2-8aca-4cda-9fd4-b1676ee73afb.png">
<img width="390" alt="image" src="https://user-images.githubusercontent.com/43568675/186592280-02679736-3b79-43e8-bd93-324a642d2bb4.png">


- [x]  模型导入

- [x]  网格划分 ICEM CFD
默认几何单位记得需要调整 

## Day 22 混合弯管二维流动和传热问题2
<img width="1055" alt="image" src="https://user-images.githubusercontent.com/43568675/186846768-23ac5764-8b48-46c3-90da-6ce308497617.png">

- [x] 网格预划分

1. 结构化/非结构化网格划分 
规则流体域，进行结构化网格
2. 网格参数设置好后，提前预览，达到要求再生成

- [x] 网格划分步骤
 blocking
* create block-命名 生成块
* split block 划分块 通过线 点 等进行划分
* associate 关联 将几何和块上的点 关联到一起
<img width="1002" alt="image" src="https://user-images.githubusercontent.com/43568675/186850483-2be2ce6d-e126-479e-a795-3f712c0742ad.png">

这段视频做得太烂了，实在是总结不下去
总结一下感受 操作繁琐，流程不明晰，暂时没搞懂为什么CFD用ICEM作为主流网格划分工具，明天换个教程看ICEM网格划分


## Day 23 ICEM软件分析

- [x] ICEM主要特点

1. 具有良好的操作界面。ICEM CFD 界面符合 windows 操作习惯。

2. 提供丰富的几何接口。其不仅支持常见的中间格式模型（如 igs、stp、parasold 等），还支持一些通用 CAD 软件（如 CATIA、NX、PRO/E、SolidWorks 等）的直接模型输入，同时还支持点数据输入。

3. 具有完善的几何操作功能。提供了一系列工具可以对输入的几何进行简化、错误检查及修复，同时还具备几何模型创建功能。

4. 网格装配。ICEM CFD 可以将复杂模型进行分解单独进行网格划分，之后将单独划分的计算网格组装成整体网格。

5. 混合网格。ICEM CFD 允许网格中包含六面体网格、四面体网格、金字塔网格以及棱柱网格。

6. 独特的虚拟块六面体网格生成功能。能够很方便地实现 O 型网格、C 型网格及 L 型网格的划分，可以显著地提高曲率较大位置的网格质量。

7. 灵活的拓扑构建方式。既可以采用自顶向下构建方式，也可以采用自底向上的拓扑构建方式。

8. 快速网格生成功能。

9. 具有多种网格质量标定功能。能快速标定及显示低于质量标准的网格，并提供了整体网格光顺、坏网格自动重划分、可视化修改网格质量等功能。

10. 拥有超过 100 种求解器接口，包括 FLUENT、CFX、CFD++、CFL3D、STAR-CD、STAR-CCM+、Nastran、Abaqus、Ls-dyna、ANSYS 等。

- [x] ICEM CFD 文件类型

文件扩展名分别为 tin、prj、uns、blk、fbc、atr、par、jrf、rpl。这些文件类型所包含的文件内容如下。

1. Tetin（*.tin）：Tin 文件包含了几何实体、材料点、创建的 part、关联信息以及网格尺寸数据。

2. Project Setting（*.prj）：包含 prject 设置数据。

3. Domain（*.uns）：包括非结构网格数据。

4. Blocking（*.blk）：保存分块拓扑结构信息。

5. Boundary Conditions（*.fbc）：包含边界条件设置数据。

6. Attributes（*.att）：包括属性、局部参数及单元类型。

7. Parameters（*.par）：包括模型参数及单元类型。

8. Journal（*.jrf）：该文件记录了用户的操作步骤。

9. Replay（*.rpl）：保存用户录制的脚本文件。

- [x] 主要优势

在 CFD 计算中，网格质量及数量直接影响计算精度与计算速度。
ICEM CFD 强大的网格划分功能可满足 CFD 计算对网格的严格要求：边界层自动加密、流场变化剧烈区域局部网格加密、高质量的全六面体网格、复杂空间的混合网格划分等。

主要优势包括以下方面。

1. 采用映射技术的六面体网格划分功能。通过雕塑方法在拓扑空间进行网格划分，然后自动映射至物理空间，可以在任意形状的模型中剖分出六面体网格。

2. 映射技术自动修补几何表面的裂缝和空洞，从而生成光滑的贴体网格。

3. 采用独特「O」型网格生成技术来生成六面体边界层网格。

4. 网格质量检查功能可以轻松检查、标识出质量差的单元。利用「网格光滑」功能可以对已有网格进行均匀化处理，从而提高网格质量。

5. ICEM CFD 提供了强大的网格编辑功能，可以对已有的网格进行编辑处理，如转化单元类型：棱柱 → 四面体、所有网格 → 四面体等

6. ICEM CFD 提供了良好的脚本运行机制，可以通过录制脚本方便地实现命令流自动处理。
