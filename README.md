在此暂不公布源代码   著作者：Cyuan
软件以文件的形式，上面可以直接下载
这是一款用于生物信息学转录组上游一键式分析的软件
注意适配的系统为Linux
处理器架构需为x86_64

首先最重要的是，由于质控和修剪步骤需要人为查看评估和修剪在此不列入其中
你需要在你的Linux系统下载一个conda软件
并且需要在你自己的conda中创建属于你的新环境
在这个新环境中依次下载此软件所需要的依赖和包，python版本最好为3.12
这些依赖（软件包）包括fastqc、hisat2、samtools、htseq、multiqc
下载后软件直接自己识别调用
(hisat2-build version 2.2.1)   (samtools 1.22.1)  htseq-count (2.0.9) (multiqc, version 1.32)
这是我所使用版本仅供参考已经证实无依赖冲突

然后在命令行中输入
chmod +x  IPFSeq3.0  #为软件加权限
./IPFSeq3.0 #运行此交互式软件

1. 标题栏
Integrated platform for quantitative sequence alignment (China Yuan)：软件名称，表明其功能是 “定量序列比对集成平台”，括号中 “China Yuan” 可能是开发标识或版本相关信息。

2. 数据输入区（Data Input）
该区域用于设置分析所需的基础数据和参数：
Working Directory (Custom): 自定义工作目录输入框，用于指定分析过程中产生的中间文件和结果文件的存储路径。右侧Browse按钮：点击可图形化选择文件夹作为工作目录。

Reference Genome File (.fa/.fasta/.fna): 参考基因组文件输入框，需输入格式为.fa、.fasta 或.fna 的基因组序列文件。右侧Browse按钮：用于选择参考基因组文件。

Fastq.gz file/directory: Fastq 格式测序数据（压缩为.gz）的文件或目录输入框，可输入单个文件路径或包含多个 fastq.gz 文件的目录。右侧Browse按钮：用于选择测序数据文件或目录。

Sequencing Mode: 测序模式选择，包含两个单选按钮：
Single-end: 单端测序模式，适用于仅一端测序的 reads 数据。
Paired-end: 双端测序模式，适用于两端都测序的成对 reads 数据。

Annotation File (.gtf/.gff/.gff3): 注释文件输入框，需输入格式为.gtf、.gff 或.gff3 的基因结构注释文件（用于后续的 reads 计数）。右侧Browse按钮：用于选择注释文件。

Threads: 线程数设置框，默认值为 8，用于指定分析过程中使用的 CPU 线程数量（数值越大，分析速度可能越快，受限于计算机性能）。
将需要输入的文件上传完整后选择单双端模式，依次点击功能流程按钮区的按钮即可分析

3. 功能流程按钮区
该区域包含序列比对分析的核心步骤按钮，按顺序执行即可完成从数据到结果的处理：
1. Build Reference Index (hisat2-build): 构建参考基因组索引按钮，点击后调用 hisat2-build 工具，基于输入的参考基因组文件生成索引（为后续比对做准备）。
2. Align Reads (hisat2): 比对 reads 按钮，调用 hisat2 工具，将测序数据（fastq.gz）与参考基因组索引进行比对，生成 SAM 格式的比对结果。
3. Process BAM (samtools): 处理 BAM 文件按钮，调用 samtools 工具，将 SAM 文件转换为 BAM（二进制格式，节省空间）并进行排序等处理。
4. Count Reads (htseq-count): 计数 reads 按钮，调用 htseq-count 工具，基于注释文件和处理后的 BAM 文件，统计每个基因的 reads 数量（用于定量分析）。
Open Results: 打开结果按钮，点击可直接查看分析生成的最终结果文件（如计数结果、报告等）。

4. 运行日志区（Run Log）
该区域实时显示软件的运行状态和日志信息：
启动时会自动检查运行环境和所需工具（如 hisat2、samtools、htseq-count 等）是否存在及可用。
显示工作目录的初始化信息，包括创建的子目录（如 mapping、output、expression 等，用于分类存储不同阶段的文件）。
后续执行各步骤时，会显示具体的运行命令、进度和可能的错误信息，帮助排查问题。

5. 底部功能按钮
Clean Working Dir: 清理工作目录按钮，点击后会删除工作目录下的中间文件和结果文件（谨慎使用，避免误删重要数据）。
总结

该软件是一个生物信息学序列比对集成工具，集成了 hisat2、samtools 等主流工具，简化了从索引构建到 reads 计数的完整流程。
使用时需依次设置工作目录、参考基因组、测序数据等基础信息，选择测序模式和线程数，再按顺序执行四个核心步骤。
