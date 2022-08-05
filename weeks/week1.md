# Week 1

## Day 1 CFD入门
> 传送门 [无痛CFD入门21讲](https://www.fangzhenxiu.com/course/1281912/1303144)

- [x] CFD基本思想，

  1. CFD基本思想  
 
  * 数学描述复杂物理问题
  * 求解方程描述流动与传热传质过程 
  * 离散求解流动方程得到流动信
  
  2. CFD发展 
  
  * 70s 航空航天 
  * 80s 多重网格技术  
  * then 粘性N-S方程 涡粘模型 DNS和LES 
  * 2020多领域结合
  
  3. 流动控制方程 
  
  * 理论解  
  * 数值解 （差分法 有限体积法 边界元法 谱方法 粒子法）
  
  4. CFD和流体力学 
  * 构建偏微分方程（建模）/求解偏微分方程（数值求解）
  * CFD是流体力学or数值算法的分支-ferziger
  
  5. 计算方式
  * 有限差分法（简单成熟，高精度格式/处理复杂网格不够灵活/相对简单外形的高精度计算）
  * 有限体积法（守恒性好，可处理复杂网格/不易提高精度，二阶以上方法复杂/复杂外形工程计算） 
  * 有限元法（基于变粉原理，守恒性好/对于复杂方程处理困难/固体力学）
  * 间断有限元法（DG）（精度高守恒性好，抑郁处理复杂网格/计算量大，捕捉激波难度大/复杂外形高精度计算）
  * 谱方法（精度高/外形，边界条件简单/简单外形高精度）
  * 粒子类方法（算法简单，可处理复杂外形/精度不易提高/复杂外形的工程计算）

- [x] CFD网格基础

  1. 网格划分工具
 
  * ICEM CFD
  * Gambit
  * Hypermesh & ANSA
  * T-Grid Fluent meshing
  * Workbench meshing
  * Pointwise
  * 开源-Salome & Gmsh Openmesh
  
  2. 网格生成一般流程

  * 准备/绘制几何
  * 定义全局尺寸
  * 定义局部尺寸
  * 网格预生成
  * 网格检查：质量评价（）
  * 网格优化
  * 网格导出 .msh
  * 网格再优化以及网格无关性验证
  
  3. 科学方法-重点区域重点处理
  * 流场变化剧烈的地方需要加密
  * 需要提高精度的地方需要加密
  * 网格增长率1.1-1.3
  
  4. 网格形状：求解器的离散算法
  
  * 离散精度
  * 几何适应性
  * （四边形和六面体网格的离散精度好，三角形和四面体的几何适应性好）
  * 相同网格数量情况下，六面体精度更高
  
- [ ] ICEM介绍







## Day 2 
> 传送门 [结构分析初中级学习路线](https://www.fangzhenxiu.com/path/20/)
> 
> [资料与模型](https://pan.baidu.com/s/1jOlaHUbQZNNBSLJka9JQsA) 提取码：jygc 

- [x] [Stack Overflow Principle](https://ctf-wiki.github.io/ctf-wiki/pwn/linux/stackoverflow/stackoverflow-basic-zh/): 
  
