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
