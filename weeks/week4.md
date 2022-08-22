## Day 18 流体有限元分析前处理知识2

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

