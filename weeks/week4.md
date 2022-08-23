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
