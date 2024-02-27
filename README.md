
# salmon定量
```
要删除data文件夹下的所有子文件夹，只保留子文件夹中的文件
可以使用find命令来查找data文件夹下的所有子文件夹，然后使用mv命令将子文件夹中的文件移动到data文件夹，最后使用rm命令删除空的子文件夹。具体的步骤如下：
打开终端，进入到data文件夹所在的目录。
输入以下命令，查找data文件夹下的所有子文件夹，并将结果保存到一个临时文件中。
find data -type d > tmp.txt
输入以下命令，读取临时文件中的每一行，将子文件夹中的文件移动到data文件夹，然后删除子文件夹。
while read line; do mv "$line"/* data; rmdir "$line"; done < tmp.txt
输入以下命令，删除临时文件。
rm tmp.txt
这样，你就可以实现你想要的效果，data文件夹下只剩下文件，没有子文件夹了。
注意：在执行上述命令之前，建议你先备份你的数据，以防万一出现意外。另外，如果你的文件名中包含空格或特殊字符，你可能需要对文件名进行转义或引用，以避免错误。
```

```
# Salmon定量 {#salmon}


cd /u3/hekun/rnaseq/2.cleandata

ls -sh *


### 4.0K compare_pair          25M trt_N080611_1.fq.gz     16M untrt_N061011_1.fq.gz
### 4.0K sampleFile            25M trt_N080611_2.fq.gz     16M untrt_N061011_2.fq.gz
###  13M trt_N052611_1.fq.gz   14M trt_N61311_1.fq.gz      19M untrt_N080611_1.fq.gz
###  13M trt_N052611_2.fq.gz   14M trt_N61311_2.fq.gz      19M untrt_N080611_2.fq.gz
###  18M trt_N061011_1.fq.gz   19M untrt_N052611_1.fq.gz   15M untrt_N61311_1.fq.gz
###  18M trt_N061011_2.fq.gz   19M untrt_N052611_2.fq.gz   15M untrt_N61311_2.fq.gz
### 
### genome:
### 总用量 87M
###  62M GRCh38.fa   24M GRCh38.gtf  1.7M GRCh38.idmap


## 测序文件下载

# 使用NCBI提供的SRA-toolkit中的工具`fastq-dump`直接下载SRR文件，并转换为`FASTQ`格式，`--split-3`参数表示如果是双端测序就自动拆分，如果是单端不受影响。

# SRA toolkit <https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=software>, 根据服务器操作系统类型下载对应的二进制编码包，下载解压放到环境变量即可使用。

# CentOS下地址：<https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.9.0/sratoolkit.2.9.0-centos_linux64.tar.gz>。

# 如果需要下载测序数据，则取消下面语句前的#
# 如果是在线学习，请取消下面的注释，自行下载
#cd ~/transcriptome/data
#fastq-dump -v --split-3 --gzip SRR1039508
#rename "SRR1039508"  "untrt_N61311"  SRR1039508*
#fastq-dump -v --split-3 --gzip SRR1039509
#rename "SRR1039509"  "trt_N61311"  SRR1039509*
#fastq-dump -v --split-3 --gzip SRR1039512
#rename "SRR1039512"  "untrt_N052611"  SRR1039512*
#fastq-dump -v --split-3 --gzip SRR1039513
#rename "SRR1039513"  "trt_N052611"  SRR1039513*
#fastq-dump -v --split-3 --gzip SRR1039516
#rename "SRR1039516"  "untrt_N080611"  SRR1039516*
#fastq-dump -v --split-3 --gzip SRR1039517
#rename "SRR1039517"  "trt_N080611"  SRR1039517*
#fastq-dump -v --split-3 --gzip SRR1039520
#rename "SRR1039520"  "untrt_N061011"  SRR1039520*
#fastq-dump -v --split-3 --gzip SRR1039521
#rename "SRR1039521"  "trt_N061011"  SRR1039521*
#rename "fastq" "fq" *.gz
#/bin/rm ~/ncbi/public/sra/*.sra

## 测序文件查看和测序量评估

# 进入data目录
cd /u3/hekun/rnaseq/2.cleandata

# 查看文件，压缩或未压缩的都可以，尤其适合查看极大文件
# 在Rstudio界面不可用, 可以查看，但不能退出
#less trt_N061011_1.fq.gz

# zcat查看gzip压缩的文件
# head -n 8 显示前8行文件内容
# 前8行是代表几条序列？
# zcat trt_N061011_1.fq.gz | head -n 8

# 测序reads数计算

# wc -l: 计算行数
# bc -l: 计算器 (-l：浮点运算)
# 为什么除以4，又除以1000000？
# echo "`zcat trt_N061011_1.fq.gz | wc -l` / (4*1000000)" | bc -l
# .464329 million

# 测序碱基数计算 (只包含20号染色体的数据) (awk的介绍见[常用和不太常用的awk命令](http://mp.weixin.qq.com/s/8wD14FXt7fLDo1BjJyT0ew))

# awk运算
# %取余数
# zcat trt_N061011_1.fq.gz | awk '{if(FNR%4==0) base+=length}END{print base/10^9,"G";}'
# 0.028816 G

## 测序质量评估 (NGS基础 - FASTQ格式解释和质量评估: https://mp.weixin.qq.com/s/tDMih7ISLJcL4F4sWBq3Vw)

fastqc trt_N061011_1.fq.gz
# trt_N061011_1_fastqc.html 在Rstudio中打开 (View in Web browser)

# 批量评估
fastqc *.fq.gz

# multiqc 整理评估结果
multiqc -d . -o multiqc

# 结果存储在multiqc/multiqc_report.html, 双击打开

## 基因注释文件准备 gtf转bed12
cd /u3/hekun/rnaseq/ref

# assembl="GRCh38"
# ucsc_assembl="hg38"

# gtf2bed12.sh所做的操作就是下面两句话
# gtfToGenePred -ignoreGroupsWithoutExons GRCh38.gtf GRCh38.gtf.50505050.pred
# genePredToBed GRCh38.gtf.50505050.pred GRCh38.gtf.bed12
# 删除临时文件
# /bin/rm -f GRCh38.gtf.50505050.pred


# gtf2bed12.sh -f GRCh38.gtf
# 选择长度适中的转录本用于后续评估
# awk '$3-$2>1000 && $3-$2<2000' GRCh38.gtf.bed12 >GRCh38.model.gtf.bed12
# head GRCh38.gtf.bed12

# # cp ../bak/GRCh38.chromsize .
# 下载chrome size文件，第一列为染色体名字，第二列为染色体大小
# 也可以自己写程序计算
# 适用于任何基因组序列，先判断是不是读到的第一条染色体，如果不是就打印；如果是只存储
# 记得输出最后一条染色体的长度信息
# awk 'BEGIN{OFS="\t"}{if($0~/>/) {if(size>0) print chrname, size; size=0; chrname=$0; sub(">","", chrname);} else size+=length;}END{print chrname,size}' GRCh38.fa
# mysql --user=genome --host=genome-mysql.cse.ucsc.edu -A -e "select chrom, size from hg38.chromInfo" | tail -n +2 >GRCh38.chromsize
# head GRCh38.chromsize


# 不基于比对的定量 (salmon)

## 获取转录本序列, (如果物种有cDNA序列提供，直接下载，如果没有则用下面的程序，通过gtf和genome文件提取)

# gffread生存的fasta文件同时包含基因名字和转录本名字
gffread GRCh38.gtf -g GRCh38.fa -w GRCh38.transcript.fa.tmp
# 去掉空格后面的字符串，保证cDNA文件中fasta序列的名字简洁，不然后续会出错
cut -f 1 -d ' ' GRCh38.transcript.fa.tmp >GRCh38.transcript.fa
head GRCh38.transcript.fa

cd /u3/hekun/rnaseq/salmon
## 构建Salmon索引

# GRCh38.transcript.fa：待分析的cDNA文件，转录本序列fasta文件
# GRCh38.salmon： salmon索引输出文件夹
#这段是易生信的，但是太简单，下列未注释的代码是根据官网重新写的全面的构建索引和定量salmon index -t GRCh38.transcript.fa -i GRCh38.salmon


gzip Taestivum.dna.toplevel.fa
gzip Taestivum.cdna.fa

#这里的cdna文件就是文档中说的转录组文件，这两条命令会将原文件压缩为.gz格式，并且删除原文件。如果您想保留原文件，您可以加上-k选项，例如：

gzip -k Taestivum.dna.toplevel.fa
gzip -k Taestivum.cdna.fa
#这两条命令会在原文件的基础上生成.gz格式的文件，但不会删除原文件。
#这里的cdna文件就是文档中说的转录组文件，这两条命令会将原文件压缩为.gz格式，并且删除原文件。如果您想保留原文件，您可以加上-k选项，例如：
grep "^>" <(gunzip -c Taestivum.dna.toplevel.fa.gz) | cut -d " " -f 1 > /u3/hekun/rnaseq/salmon/decoys.txt
sed -i.bak -e 's/>//g' /u3/hekun/rnaseq/salmon/decoys.txt
cat Taestivum.cdna.fa.gz Taestivum.dna.toplevel.fa.gz > /u3/hekun/rnaseq/salmon/gentrome.fa.gz
cd  /u3/hekun/rnaseq/salmon
salmon index -t gentrome.fa.gz -i salmon_Taestivum_index --d decoys.txt -p 12 -k 31

# 定量
for fn in /u3/hekun/rnaseq/2.data_qc/*_1.clean.fastp.fq.gz;
do 
i=`basename ${fn} _1.clean.fastp.fq.gz`
echo "Processing sample ${i}"

salmon --no-version-check quant -i salmon_Taestivum_index -l A \
         -1 /u3/hekun/rnaseq/2.data_qc/${i}_1.clean.fastp.fq.gz \
         -2 /u3/hekun/rnaseq/2.data_qc/${i}_2.clean.fastp.fq.gz \
         --gcBias --seqBias \
         -p 20 --validateMappings -o quants/${i}_quant
done &

echo "
Version Server Response: Not Found，这不会影响结果。这个问题只是和版本检查有关，和定量分析的算法和数据无关。如果不想要则加上--no-version-check
# 三文鱼索引需要基因组目标的名称，可以使用以下grep命令提取该名称：

grep "^>" <(gunzip -c Taestivum.dna.toplevel.fa.gz) | cut -d " " -f 1 > decoys.txt
#grep是一种用于在文本中搜索匹配模式的命令
#"^>"是一个正则表达式，表示以>符号开头的行
#<(gunzip -c Taestivum.dna.toplevel.fa.gz)是一个进程替换，表示将gunzip命令的输出作为一个文件传递给grep
#gunzip是一种用于解压缩.gz格式的文件的命令
#-c选项表示将解压缩的内容输出到标准输出，而不是覆盖原文件
#Taestivum.dna.toplevel.fa.gz是一个压缩的FASTA格式的文件，包含了小麦的基因组序列
#|是一个管道符号，表示将前一个命令的输出作为后一个命令的输入
#cut是一种用于按照分隔符切分文本的命令
#-d " "选项表示以空格为分隔符
#-f 1选项表示只保留第一个字段
#> decoys.txt表示将cut命令的输出重定向到一个名为decoys.txt的文件中
#decoys.txt文件中存储了基因组目标的名称，也就是鲑鱼索引中的诱饵,**经过重现官方文档步骤，其实就是染色体的名称**

sed -i.bak -e 's/>//g' decoys.txt
#sed是一种用于对文本进行编辑的命令
#-i.bak选项表示对原文件进行修改，并且保存一个备份文件，后缀为.bak
#-e选项表示执行一个编辑命令
#'s/>//g'是一个替换命令，表示将每一行中的>符号替换为空，g表示全局替换
#这一步的目的是去掉decoys.txt文件中每一行开头的>符号，使得诱饵的名称与鲑鱼索引中的一致

#除了诱饵列表之外，鲑鱼还需要串联的转录组和基因组参考文件作为索引。注意：基因组目标（诱饵）应位于转录组目标之后
#除了诱饵列表之外，鲑鱼还需要串联的转录组和基因组参考文件作为索引。注意：基因组目标（诱饵）应位于的转录组目标之后

#这一段是说，鲑鱼索引中的目标文件是由两个文件合并而成的，一个是转录组文件，一个是基因组文件。转录组文件包含了所有的转录本序列，基因组文件包含了所有的染色体序列。
#鲑鱼索引的原理是使用一种叫做轻量级比对（lightweight-alignment）的方法，来快速准确地从RNA-seq数据中估计转录本的丰度。这种方法的关键是利用一种叫做诱饵（decoy）的技术，来避免将RNA-seq读段错误地比对到基因组上，而不是转录组上。
#诱饵就是指那些可能与转录本序列相似，但不属于转录本的基因组序列，它们通常是一些未注释的基因或转座子等。诱饵的作用是在比对过程中，将那些可能比对到多个位置的读段过滤掉，从而提高比对的准确性和转录本的丰度估计的可靠性。
#为了使用诱饵技术，鲑鱼索引需要两个输入文件，一个是目标文件，一个是诱饵文件。目标文件就是包含了转录组和基因组的文件，诱饵文件就是包含了基因组目标（诱饵）的名称的文件。这两个文件的内容和格式可以参考这里。
#在目标文件中，为了让鲑鱼索引能够正确地识别诱饵，需要将基因组目标放在转录组目标之后，也就是说，先写转录本的序列，再写染色体的序列。这样，鲑鱼索引就会优先比对转录本，然后再比对诱饵，从而过滤掉那些不确定的读段。

cat Taestivum.cdna.fa.gz Taestivum.dna.toplevel.fa.gz > gentrome.fa.gz（其实就是cdna文件最后加让了染色体名称））
#cat是一种用于连接文件内容的命令
#Taestivum.cdna.fa.gz是一个压缩的FASTA格式的文件，包含了小麦的转录组序列
#Taestivum.dna.toplevel.fa.gz是一个压缩的FASTA格式的文件，包含了小麦的基因组序列
#> gentrome.fa.gz表示将cat命令的输出重定向到一个名为gentrome.fa.gz的文件中
#gentrome.fa.gz文件中存储了串联的转录组和基因组参考文件，也就是鲑鱼索引中的目标

#鲑鱼索引
#我们已经准备好鲑鱼食谱的所有原料。我们可以按如下方式运行鲑鱼索引步骤：

salmon index -t gentrome.fa.gz -d decoys.txt -p 12 -i salmon_Taestivum_index --gencode
（gentrome.fa.gz等价于Taestivum.cdna.fa.gz。转录本文件即transcripts.fa）
#salmon是一种用于转录组定量的工具，可以通过命令行运行
#index是一个子命令，表示构建鲑鱼索引
#-t gentrome.fa.gz选项表示指定目标文件，也就是串联的转录组和基因组参考文件
#-d decoys.txt选项表示指定诱饵文件，也就是基因组目标的名称
#-p 12选项表示指定使用的线程数，也就是并行运行的进程数
#-i salmon_Taestivum_index选项表示指定索引的输出目录，也就是索引文件的存储位置
#--gencode选项表示删除目标标头中|与 gencode 引用分隔的额外元数据，这是因为转录组参考文件是从gencode数据库下载的，如果使用其他参考，您可以跳过它

#注意：--gencode标志用于删除目标标头中|与 gencode 引用分隔的额外元数据。如果使用其他参考，您可以跳过它。
#–gencode选项表示删除目标标头中|与 gencode 引用分隔的额外元数据，这是因为转录组参考文件是从gencode数据库下载的，如果使用其他参考，您可以跳过它
#这一段是说，鲑鱼索引中的目标文件是由转录组和基因组两部分组成的，而转录组文件是从一个叫做gencode的数据库下载的。gencode是一个项目，它的目标是识别和分类人类和小鼠基因组中的所有基因特征1。
#gencode数据库提供的转录组文件中，每个转录本的标识符（ID）都是由一些元数据组成的，这些元数据包括转录本的类型、来源、版本等信息，它们之间用|符号分隔。例如，ENST00000456328.2|ENSG00000223972.5|OTTHUMG00000000961.2|OTTHUMT00000002844.2|DDX11L1-202|DDX11L1|1657|processed_transcript|2。
#鲑鱼索引中只需要用到转录本的ID，而不需要这些额外的元数据，所以使用–gencode选项可以去掉|符号后面的部分，只保留ENST00000456328.2这样的ID。
#如果您使用的转录组文件不是从gencode数据库下载的，那么您不需要使用这个选项，因为您的文件中可能没有这些额外的元数据，或者它们的格式不同。
一个较小的 k 值可能会稍微提高灵敏度。灵敏度是指正确比对的 reads 占所有真实比对的 reads 的比例，它反映了比对算法的查全率。一个较小的 k 值意味着更容易找到有效的匹配，从而提高灵敏度。
We find that a k of 31 seems to work well for reads of 75bp or longer, but you might consider a smaller k if you plan to deal with shorter reads.
这句话的意思是，我们发现，对于长度为 75bp 或更长的 reads，一个 k 值为 31 的索引似乎工作得很好，但是如果您打算处理更短的 reads，您可能需要考虑一个更小的 k 值。这是因为，对于更短的 reads，一个较大的 k 值可能会导致找不到有效的匹配，从而降低灵敏度。
Also, a shorter value of k may improve sensitivity even more when using selective alignment (enabled via the –validateMappings flag).
这句话的意思是，另外，当使用 selective alignment 时，一个较短的 k 值可能会更加提高灵敏度（通过 --validateMappings 标志来启用）。
"

# salmon索引目录下的内容
ls salmon_Taestivum_index

# duplicate_clusters.tsv  hash.bin  header.json  indexing.log  quasi_index.log  
# refInfo.json  rsd.bin  sa.bin  txpInfo.bin  versionInfo.json

# 有些转录本名字不同，但序列完全一样，被鉴定出来只保留一个。
head salmon_Taestivum_index/duplicate_clusters.tsv 

# RetainedTxp	DuplicateTxp
# ENST00000486475	ENST00000629881
# ENST00000401322	ENST00000637366
# ENST00000401322	ENST00000401376
# ENST00000401322	ENST00000621667


# 注意切换目录
# 定量（上面已完成）
# cd /u3/hekun/rnaseq/salmon

# mkdir -p trt_N061011
# 在读取文件之前，应在命令行上指定库类型 -l（即 -1 和 -2 或 -r 的参数）。这是因为库类型标志的内容用于确定应如何解释读取。
# 或者，在任何情况下，您都可以简单地使用 --gcBias 运行 Salmon，因为它不会影响没有 GC 偏差的样品的定量，每个样品只需要多花几分钟。对于具有中度至高度 GC 偏倚的样品，在片段水平 ha 上对这种偏倚进行校正
# salmon quant --gcBias -l A -1 trt_N061011_1.fq.gz -2 trt_N061011_2.fq.gz  -i genome/GRCh38.salmon -o trt_N061011/trt_N061011.salmon.count -p 4


# 输出结果存储在 trt_N061011/trt_N061011.salmon.count目录中
# quant.sf 为转录本表达定量结果，第4列为TPM结果，第5列为reads count
# quant.genes.sf 为基因表达定量结果
head trt_N061011/trt_N061011.salmon.count/quant.sf

cd /u3/hekun/rnaseq/salmon

# TAB键分割的样品分组信息
# 这里是为了在流程中，方便操作
# 实际上可以用任何文本编辑工具或者excel导出一个TAB键分割的文件，
# 第一列是样本名字
# 后面的列是样本分组或其它熟悉信息，记录越全越好
# cat <<END 输入内容 END 输入结束
# sed 's/|/\t/g': 把文件中所有的 | 替换为 \t
# sed 's/original/replace/g'
#这里的Samp会成为绘制热推的行列名，很拥挤，以后起名字应该简单些
cat <<END | sed 's/|/\t/g' >sampleFile
Samp|conditions
ANTF1_FRAS202191140-1r|AN
ANTF2_FRAS202191141-1r|AN
ANTF3_FRAS202191142-1r|AN
D10TF1_FRAS202191146-1r|D10
D10TF2_FRAS202191147-1r|D10
D10TF3_FRAS202191148-1r|D10
D15TF1_FRAS202191149-1r|D15
D15TF2_FRAS202191150-1r|D15
D15TF3_FRAS202191151-1r|D15
D20TF1_FRAS202191152-1r|D20
D20TF2_FRAS202191153-1r|D20
D20TF3_FRAS202191154-1r|D20
D25TF1_FRAS202191155-1r|D25
D25TF2_FRAS202191156-1r|D25
D25TF3_FRAS202191157-1r|D25
D30TF1_FRAS202191158-1r|D30
D30TF2_FRAS202191159-2r|D30
D30TF3_FRAS202191160-1r|D30
D35TF1_FRAS202191161-1r|D35
D35TF2_FRAS202191162-1r|D35
D35TF3_FRAS202191163-1r|D35
D5TF1_FRAS202191143-1r|D5
D5TF2_FRAS202191144-1r|D5
D5TF3_FRAS202191145-1r|D5
GATF1_FRAS202191128-1r|GA
GATF2_FRAS202191129-1r|GA
GATF3_FRAS202191130-1r|GA
HDTF1_FRAS202191137-1r|HD
HDTF2_FRAS202191138-1r|HD
HDTF3_FRAS202191139-1r|HD
TPTF1_FRAS202191134-1r|TP
TPTF2_FRAS202191135-1r|TP
TPTF3_FRAS202191136-1r|TP
YATF1_FRAS202191131-1r|YA
YATF2_FRAS202191132-1r|YA
YATF3_FRAS202191133-1r|YA
END


# 批量定量（上面已完成）
# cd /u3/hekun/rnaseq/2.cleandata
# for i in `tail -n +2 sampleFile | cut -f 1`
# 从第二行开始读，并取第一列
# do
#   salmon quant -l A -1 ${i}_1.fq.gz -2 ${i}_2.fq.gz  -i genome/GRCh38.salmon \
#     -o ${i}/${i}.salmon.count -p 4
# done
# 
# for i in `tail -n +2 sampleFile | cut -f 1`
# do
#   echo "salmon quant -l A -1 ${i}_1.fq.gz -2 ${i}_2.fq.gz  -i genome/GRCh38.salmon -o ${i}/${i}.salmon.count -p 4"
# done


# 批量定量（上面已完成）
# -g genome/GRCh38.gtf: 同时输出基因的定量结果，默认只有转录本定量结果
cd /u3/hekun/rnaseq/2.cleandata
for i in `tail -n +2 sampleFile | cut -f 1`
# 从第二行开始读，并取第一列
do
  salmon quant --gcBias -l A -1 ${i}_1.fq.gz -2 ${i}_2.fq.gz  -i genome/GRCh38.salmon \
    -o ${i}/${i}.salmon.count -p 4 >${i}.salmon.log 2>&1
  # 给每个结果增加样本信息，方便后续合并
done &



# for i in `tail -n +2 sampleFile | cut -f 1`
# do
#   echo "salmon quant --gcBias -l A -1 ${i}_1.fq.gz -2 ${i}_2.fq.gz  -i genome/GRCh38.salmon -g genome/GRCh38.gtf -o ${i}/${i}.salmon.count -p 4 >${i}.salmon.log 2>&1"
# done

# 利用multiqc整理salmon的输出日志

# -f覆盖之前的日志
multiqc -f -d . -o multiqc/


#[INFO   ]         multiqc : This is MultiQC v1.6
#[INFO   ]         multiqc : Template    : default
#[INFO   ]         multiqc : Prepending directory to sample names
#[INFO   ]         multiqc : Searching '.'
#Searching 188 files..  [####################################]  100%             
#[INFO   ]           rseqc : Found 2 read_distribution reports
#[INFO   ]          salmon : Found 8 meta reports
#[INFO   ]          salmon : Found 8 fragment length distributions
#[INFO   ]          fastqc : Found 16 reports
#[INFO   ]         multiqc : Compressing plot data
#[WARNING]         multiqc : Previous MultiQC output found! Adjusting filenames..
#[WARNING]         multiqc : Use -f or --force to overwrite existing reports instead
#[INFO   ]         multiqc : Report      : multiqc/multiqc_report.html
#[INFO   ]         multiqc : Data        : multiqc/multiqc_data_1
#[INFO   ]         multiqc : MultiQC complete




cd /u3/hekun/rnaseq/salmon
# 列出salmon的输出文件
find . -name quant.sf
# ./trt_N080611/trt_N080611.salmon.count/quant.sf
# ./trt_N061011/trt_N061011.salmon.count/quant.sf
# ./untrt_N61311/untrt_N61311.salmon.count/quant.sf

# 这个压缩包下载解压到本地，这是为了下载到电脑上，服务器分析就不用，如果用电脑R分析，则需要
zip salmon.output.zip `find . -name quant.sf`

# 这一步不用了，使用我写的另一个步骤导入，生成一个两列文件方便R导入
# xargs接收上一步的输出，按批次提供给下游程序作为输入
# -i: 用{}表示传递的值
cut -f 1 sampleFile | xargs -i echo -e "{}\tquants/{}_quant/quant.sf" >salmon.output
head salmon.output
# Samp    quants/Samp_quant/quant.sf
# ANTF1_FRAS202191140-1r   quants/ANTF1_FRAS202191140-1r_quant/quant.sf
# ANTF2_FRAS202191141-1r   quants/ANTF2_FRAS202191141-1r_quant/quant.sf




# 如果没有GTF文件，可以用其他文件，只需获取转录本和基因名字对应关系就可以
# 如果不知道对应关系，也可以把每个转录本当做一个基因进行分析
# 注意修改$14, $10为对应的信息列，
# tx2gene为一个两列文件，第一列是转录本没名字，第二列是基因名字。
#sed 's/"/\t/g' genome/GRCh38.gtf | \ # <1> 使用 sed 命令将 genome/GRCh38.gtf 文件中的双引号替换为制表符，并将结果输出到管道
#  awk 'BEGIN{OFS=FS="\t"}{if(FNR==1) print "TXname\tGene"; if($3=="transcript") print $14, $10}' >genome/GRCh38.tx2gene # <2> 使用 awk 命令从管道中读取数据，设置输出字段分隔符和输入字段分隔符为制表符，在输出文件第一行，则打印标题行，如果是第三列为 transcript 的行，则打印第十四列和第十列，即转录本名和基因名，并将结果重定向到 genome/GRCh38.tx2gene 文件中
# head genome/GRCh38.tx2gene # <3> 使用 head 命令显示 genome/GRCh38.tx2gene 文件的前十行
#要使用ensemble下载的最新版，不要用自己使用gff生成的，还有基因和转录本id要根据文件自己去数一数在第几列，不同情况下可能不同
sed 's/"/\t/g' /u3/hekun/rnaseq/salmon/Triticum_aestivum.IWGSC.58.gtf | \
  awk 'BEGIN{OFS=FS="\t"}{if(FNR==1) print "TXname\tGene"; if($3=="transcript") print $12, $10}' >/u3/hekun/rnaseq/salmon/Taestivum.58.tx2gene
head Taestivum.58.tx2gene
# TXname  Gene
# ENST00000608838 ENSG00000178591
# ENST00000382410 ENSG00000178591
# ENST00000382398 ENSG00000125788
# ENST00000542572 ENSG00000125788
#使用conda安装R包devtools，用来在R中安装GitHub上的包
conda install conda-forge::r-devtools

至此就完成了基于Salmon的所有样本基因和转录本的定量。
```





# DESeq2分析salmon所得的数据




## salmon. DESeq2.simplest. Rmd

```
#在linux中#使用conda安装R包devtools，用来在R中安装GitHub上的包
conda install conda-forge::r-devtools
# R代码，在本地windows运行,
#安装R包报错：

#grab failed: window not viewable.

#Error in structure(.External(.C_dotTclObjv, objv), class = "tclObj") : 
#[tcl] grab failed: window not viewable.
#一般发生在远程linux系统中安装R包，是因为R调用窗口失败，解决方法是
# chooseCRANmirror(graphics=FALSE)
```

```{r}
# 需要的R包安装
BiocManager::install(version = "3.18")
BiocManager::install("tximport")

#安装YSX包 (已改名为ImageGP包)
#不推荐老的名字的包
#devtools::install_github("Tong-Chen/YSX")
#library("YSX")
# 安装好之后，之前教程的library(YSX)都改为library(ImageGP)，YSX包中的函数都可以在ImageGP包中找到，如果同时载入，R会优先使用后载入包的函数
devtools::install_github("Tong-Chen/ImageGP")
 

if (!require("BiocManager", quietly = TRUE))
install.packages("BiocManager")
BiocManager::install("rnaseqGene")

install.packages("gplots")
install.packages("amap")
install.packages("ggrepel")

library("ggrepel")
library(rnaseqGene)
library(DESeq2)
library("RColorBrewer")
library("gplots")
library("amap")
library("ggplot2")
library("BiocParallel")
library("ImageGP")

```


```{r}
#所有输出结果的前缀，根据需要修改
output_prefix = "longchun"
file = "salmon.output"
sampleFile = "sampleFile"
design="conditions"
tx2gene="Taestivum.58.tx2gene"
type="salmon"
padj=0.05
log2FC=1
```

```{r}
DESeq2_ysx(file, sampleFile, design=design, type=type, tx2gene=tx2gene, 
           output_prefix=output_prefix, padj=padj, log2FC=log2FC)
```

#至此，salmon. DESeq2.simplest. Rmd已结束
































## salmon. DESeq2.simpler. Rmd
```
# R代码，在本地windows运行,
#安装R包报错：

#grab failed: window not viewable.

#Error in structure(.External(.C_dotTclObjv, objv), class = "tclObj") : 
#[tcl] grab failed: window not viewable.
#一般发生在远程linux系统中安装R包，是因为R调用窗口失败，解决方法是
# chooseCRANmirror(graphics=FALSE)
```

```{r}
# 需要的R包安装
BiocManager::install(version = "3.18")
BiocManager::install("tximport")

#安装YSX包 (已改名为ImageGP包)
#不推荐老的名字的包
#devtools::install_github("Tong-Chen/YSX")
#library("YSX")
# 安装好之后，之前教程的library(YSX)都改为library(ImageGP)，YSX包中的函数都可以在ImageGP包中找到，如果同时载入，R会优先使用后载入包的函数
devtools::install_github("Tong-Chen/ImageGP")
 library("ImageGP")

if (!require("BiocManager", quietly = TRUE))
install.packages("BiocManager")
BiocManager::install("rnaseqGene")
library(rnaseqGene)

install.packages("gplots")
install.packages("amap")
install.packages("ggrepel")

library(DESeq2)
library("RColorBrewer")
library("gplots")
library("amap")
library("ggplot2")
library("BiocParallel")
library("ImageGP")

```

```{r}
library(DESeq2)
library("RColorBrewer")
library("gplots")
library("amap")
library("ggplot2")
library("BiocParallel")
library("ImageGP")
```

##初始化，定义输入、输出和参数

```{r}
# Prefix for all output file 
output_prefix = "longchun"

# pipelineSalmon.sh生成的一个两列文件，第一列是样品名字，第二列是salmon定量结果的位置，注意第二列文件的路径
file = "salmon.output"
# 分组信息表
sampleFile = "sampleFile"
# 分组信息所在列名字
design="conditions"
# 转录本和基因的对应关系
tx2gene="genome/GRCh38.tx2gene"
# 输入数据类型，salmon结果或reads count 矩阵
type="salmon"
# 差异基因参数
padj=0.05
log2FC=1
```
##数据读入和标准化

```{r}
dds <- salmon2deseq(file, sampleFile, design=design, tx2gene=tx2gene)
normexpr <- deseq2normalizedExpr(dds)
```
##检查标准化后数据的分布

```{r}
# normalizedExpr2DistribBoxplot(normexpr, 
#                               saveplot=paste(output_prefix, "DESeq2.normalizedExprDistrib.pdf", sep="."))
normalizedExpr2DistribBoxplot(normexpr)
```

##样本聚类

```{r}
# clusterSampleHeatmap2(normexpr$rlog, 
#                       cor_file=paste(output_prefix, "DESeq2.sampleCorrelation.txt", sep="."), 
#                       , sep="."))
clusterSampleHeatmap2(normexpr$rlog[1:5000,], cor_file=paste(output_prefix, "DESeq2.sampleCorrelation.txt", sep="."), saveplot=paste(output_prefix, "DESeq2.sampleCorrelation.pdf"))
clusterSampleUpperTriPlot(normexpr$rlog[1:5000,], cor_file=paste(output_prefix, "DESeq2.sampleCorrelation.txt", sep="."))
```

```{r}
multipleGroupDEgenes(dds, design=design, output_prefix=output_prefix, padj=padj, log2FC=log2FC)
```

##Replot

```{r}
res_output <- read.table("ehbio.DESeq2.trt._vs_.untrt.results.xls", header=T, row.names=1)
groupA = 'trt'
groupB = 'untrt'
res_output$level <- ifelse(res_output$padj<=padj,
                             ifelse(res_output$log2FoldChange>=log2FC,
                                    paste(groupA,"UP"),
                             ifelse(res_output$log2FoldChange<=(-1)*(log2FC),
                                    paste(groupB,"UP"), "NoDiff")) , "NoDiff")
volcanoPlot(res_output, "log2FoldChange", "padj",
              "level")

rankPlot(res_output, label=10, width=20)
```

```{r}
a <- c("Pou5f1","Gata4")
names(a) <-  c("ENSG00000116584","ENSG00000256235")
rankPlot(res_output, label=a, width=20)
```
```{r}
rankPlot
```


```{r}
data_line <- data[order(data[[order_col]]),,drop=F]
  row_num <- nrow(data_line)
  data_line$x <- 1:row_num
  data_line$xend <- 2:(row_num+1)
  if(!is.null(label)){
    if (length(label) == 1 & is.numeric(label)) {
      # Label top
      data_line$id__ct <- rownames(data_line)
      data_line[(label+1):(row_num-label),"id__ct"] <- NA
    } else {
      if(is.null(names(label))){
        # Label given ids
        data_line$id__ct <- NA
        data_line$id__ct <- label[match(rownames(data_line), label)]
      } else {
        # Label substitute ids
        data_line$id__ct <- NA
        data_line$id__ct <- label[match(rownames(data_line), names(label))]
      }
    }
  }


  p <- ggplot(data_line) +
    geom_segment(aes_string(x="x", xend="x",y=order_col,yend=0, color=order_col), alpha=alpha)
  #geom_linerange(aes_string(x="x", ymin=order_col,ymax=0, color=order_col), alpha=alpha)
  #geom_rect(aes_string(xmin="x", xmax="xend",ymin=order_col,ymax=0, fill=order_col), alpha=alpha)

  if(length(colorvector)==2){
    p <- p + scale_color_gradient(low=colorvector[1], high=colorvector[2])
  } else if(length(colorvector)==3){
    #names(colorvector) <- c("low","mid","high")
    #colorvector <- as.list(colorvector)
    #p <- p + scale_color_gradient2(colorvector, midpoint = midpoint)
    p <- p + scale_color_gradient2(low=colorvector[1], mid=colorvector[2],
                                   high=colorvector[3], midpoint = midpoint)
  } else {
    stop("Illegel color vector.")
  }
  p <- p + theme_classic() + geom_hline(yintercept = midpoint, linetype="dotted")

  if(!is.null(label)){
    # 标记基因名字
    p <- p + ggrepel::geom_text_repel(aes_string(x="x", y=order_col, label="id__ct"))
  }

  if(!is.null(saveplot)){
    ggsave(plot=p, filename=saveplot, units=c("cm"),...)
  }

  return(p)

}
```

```{r}
a <- data.frame(log2FoldChange=rnorm(1000), row.names=paste0("YSX",1:1000))

## Raw plot

rankPlot(a)

## Label top 10

rankPlot(a, label=10)

## Label specified points

rankPlot(a, label=c("YSX1","YSX2","YSX10"))

## Label specified points with new names

b <- c("A","B","C")
names(b) <- c("YSX1","YSX2","YSX10")
rankPlot(a, label=b)

```
#至此，salmon. DESeq2.simpler. Rmd已结束




















## salmon. DESeq2. Rmd
```
# R代码，在本地windows运行,
#安装R包报错：

#grab failed: window not viewable.

#Error in structure(.External(.C_dotTclObjv, objv), class = "tclObj") : 
#[tcl] grab failed: window not viewable.
#一般发生在远程linux系统中安装R包，是因为R调用窗口失败，解决方法是
# chooseCRANmirror(graphics=FALSE)
```

```{r}
# 需要的R包安装
BiocManager::install(version = "3.18")
BiocManager::install("tximport")

#安装YSX包 (已改名为ImageGP包)
#不推荐老的名字的包
#devtools::install_github("Tong-Chen/YSX")
#library("YSX")
# 安装好之后，之前教程的library(YSX)都改为library(ImageGP)，YSX包中的函数都可以在ImageGP包中找到，如果同时载入，R会优先使用后载入包的函数
devtools::install_github("Tong-Chen/ImageGP")
library("ImageGP")

if (!require("BiocManager", quietly = TRUE))
install.packages("BiocManager")
BiocManager::install("rnaseqGene")
library(rnaseqGene)

install.packages("gplots")
install.packages("amap")
install.packages("ggrepel")

library(DESeq2)
library("RColorBrewer")
library("gplots")
library("amap")
library("ggplot2")
library("BiocParallel")
library("ImageGP")



# Salmon定量结果差异分析

在windows的`Rstudio`和远程访问Linux的`Rstudio`时都可以运行。
```
```

```{r, include=F}
knitr::opts_chunk$set(echo = T, out.width="100%", fig.align="center", fig.show="hold", warning=FALSE, message=FALSE)
knitr::opts_chunk$set(cache=TRUE, autodep=TRUE)
#Sys.setlocale(, 'Chinese')
```

##基因表达标准化

不同样品的测序量会有差异，最简单的标准化方式是计算 `counts per million (CPM)`，即原始`reads count`除以总reads数乘以1,000,000。

这种计算方式的缺点是容易受到极高表达且在不同样品中存在差异表达的基因的影响；这些基因的打开或关闭会影响到细胞中总的分子数目，可能导致这些基因标准化之后就不存
在表达差异了，而原本没有差异的基因标准化之后却有差异了。

RPKM、FPKM和TPM是CPM按照基因或转录本长度归一化后的表达，也会受到这一影响。

```{r calc-cpm, eval=FALSE, echo=T}
calc_cpm <- function (expr_mat, spikes = NULL){
  norm_factor <- colSums(expr_mat[-spikes,])
  return(t(t(expr_mat)/norm_factor)) * 10^6
}
```

为了解决这一问题，研究者提出了其它的标准化方法。

**量化因子 (size factor, SF)**是由`DESeq`提出的。其方法是首先计算每个基因在所有样品中表达的几何平均值。每个细胞的量化因子(size factor)是所有基因与其在所有样
品中的表达值的几何平均值的比值的中位数。由于几何平均值的使用，只有在所有样品中表达都不为0的基因才能用来计算。这一方法又被称为 **RLE (relative log expression)**。

```{r calc-sf, eval=FALSE, echo=T}
calc_sf2 <- function (expr_mat, spikes=NULL){
  geomeans <- exp(rowMeans(log(expr_mat)))
  SF <- function(cnts){
    median((cnts/geomeans)[(is.finite(geomeans) & geomeans >0)])
  }
  norm_factor <- apply(expr_mat,2,SF)
  return(t(t(expr_mat)/norm_factor))
}
```

##模拟获得size factor

```{r}
matrix <- matrix(sample(0:10,16, replace=T),nrow=4)
rownames(matrix) <- paste0("Gene",1:nrow(matrix))
colnames(matrix) <- paste0("Samp",1:ncol(matrix))
matrix
```

```{r}
matrix_log <- log(matrix)
matrix_log
matrix_rowmeans <- rowMeans(matrix_log)
matrix_rowmeans

geo_means <- exp(matrix_rowmeans)
geo_means
```

```{r}
matrix[,1]/geo_means
```

```{r}
apply(matrix, 2, function(cnts){(cnts/geo_means)})
```

```{r}
norm_factor = apply(matrix, 2, function(cnts){median((cnts/geo_means)[(is.finite(geo_means) & geo_means >0)])})
```

```{r}
norm_factor
```

```{r}
t(t(matrix)/norm_factor)
```

跟DESeq2自己的size factor函数比较

```{r}
library(DESeq2)
estimateSizeFactorsForMatrix(matrix)
```


**上四分位数 (upperquartile, UQ)**是样品中所有基因的表达除以处于上四分位数的基因的表达值。同时为了保证表达水平的相对稳定，计算得到的上四分位数值要除以所有样
品中上四分位数值的中位数。

```{r calc-uq, eval=FALSE, echo=T}
calc_uq <- function (expr_mat, spikes=NULL){
  UQ <- function(x) {
    quantile(x[x>0],0.75)
  }
  uq <- unlist(apply(expr_mat[-spikes,],2,UQ))
  norm_factor <- uq/median(uq)
  return(t(t(expr_mat)/norm_factor))
}
```

**TMM**是M-值的加权截尾均值。选定一个样品为参照，其它样品中基因的表达相对于参照样品中对应基因表达倍数的log2值定义为M-值。随后去除M-值中最高和最低的30%，剩下
的M值计算加权平均值。每一个非参照样品的基因表达值都乘以计算出的TMM。这个方法假设大部分基因的表达是没有差异的。

##安装依赖的包

```{r, eval=F, echo=T}
if (FALSE){
	source("https://bioconductor.org/biocLite.R")
	options(BioC_mirror="http://mirrors.ustc.edu.cn/bioc/")
	biocLite(c("DESeq2","BiocParallel", "tximport"))
	site= "https://mirrors.tuna.tsinghua.edu.cn/CRAN"
	install.packages(c("RColorBrewer", "gplots", "amap", "reshape2", "ggplot2", "ggrepel", "pheatmap", repos=site))
}
```

##加载依赖的包

```{r, include=F}
library("RColorBrewer")
suppressMessages(library("gplots"))
library("amap") 
library("reshape2")
library("ggplot2")
library("ggrepel")
library("pheatmap")
suppressMessages(library(DESeq2))
library("BiocParallel")
library("tximport")
library("readr")
```

##文件准备

代码来源于流程`pipeline_salmon.sh`，以其为准。

```{r, echo=F}
knitr::include_graphics("salmon_result_for_deseq2.png")
```

##初始化

使用时只需要修改 `salmon.output`和`sampleFile` 即可。分组信息列必须是`conditionds`，如果不是，下面代码中的`conditions`也需相应的修改。这两个文件的获得见`12-转录组分析流程Salmon.pdf`的`整理Salmon结果`部分。


```{r}
# 所有输出结果的前缀，根据需要修改
ehbio_output_prefix = "ehbio_salmon"
ehbio_salmon_file_init = "salmon.output"
# 分组信息列必须是`conditionds`，如果不是，下面代码中的`conditions`也许相应的修改
ysx_sampleFile_init = "sampleFile"
ysx_tx2gene_init = "genome/GRCh38.tx2gene"
```

读入数据并进行过滤 (若基因的reads count总和小于样品数的一半则过滤掉。过滤基因是为了去除低表达基因，减少建模所需时间和增加统计检测的强度)。DESeq2运行过程中也会进一步过滤，去掉那些不用统计检测也能看出的没有差异的基因。

```{r}
salmon_file <- read.table(ehbio_salmon_file_init, header=T,  row.names=1, sep="\t")
salmon_file_rowname <- rownames(salmon_file)
salmon_file <- as.vector(salmon_file[,1])
names(salmon_file) <- salmon_file_rowname
tx2gene <- read.table(ysx_tx2gene_init, header=T, row.names=NULL, sep="\t")
# 整合读入的salmon文件和transcript2gene文件
txi <- tximport(salmon_file, type = "salmon", tx2gene = tx2gene)

sample <- read.table(ysx_sampleFile_init, header=T, row.names=1, com='',
	quote='', check.names=F, sep="\t")
sample <- sample[match(colnames(txi$counts), rownames(sample)),, drop=F]


dds <- DESeqDataSetFromTximport(txi, colData=sample, design= ~conditions)
print(paste("Read in", nrow(dds),"genes"))
keep <- rowSums(counts(dds))>nrow(sample)/2
dds <- dds[keep,]
print(paste(nrow(dds),"genes remained after filtering of genes with all counts less than", nrow(sample)/2, "in all samples"))
```

##差异分析

```{r}
dds <- DESeq(dds)
```

##输出标准化后的结果

标准化后的结果按整体差异大小排序，同时输出对数转换的结果。

```{r}
# Get normalized counts
print("Output normalized counts")
normalized_counts <- counts(dds, normalized=TRUE)

# 标准化的结果按整体差异大小排序
normalized_counts_mad <- apply(normalized_counts, 1, mad)
normalized_counts <- normalized_counts[order(normalized_counts_mad, decreasing=T), ]

# 常规R输出忽略左上角（输出文件第一列也就是基因列的列名字）
# 输出结果为完整矩阵，保留左上角的id。
normalized_counts_output = data.frame(id=rownames(normalized_counts), normalized_counts)
write.table(normalized_counts_output, file=paste0(ehbio_output_prefix,".DESeq2.normalized.xls"),
quote=F, sep="\t", row.names=F, col.names=T)


rld <- rlog(dds, blind=FALSE)
rlogMat <- assay(rld)
rlogMat <- rlogMat[order(normalized_counts_mad, decreasing=T), ]


print("Output rlog transformed normalized counts")
rlogMat_output = data.frame(id=rownames(rlogMat), rlogMat)
write.table(rlogMat_output, file=paste0(ehbio_output_prefix,".DESeq2.normalized.rlog.xls"),
quote=F, sep="\t", row.names=F, col.names=T)
```

##标准化后样品的表达分布

```{r}
rlog_mat_melt <- melt(rlogMat_output, id.vars = c('id'))
ggplot(rlog_mat_melt, aes(x=variable, y=value)) + geom_boxplot(aes(color=variable)) +
  geom_violin(aes(fill=variable), alpha=0.5) + theme_classic() +
  theme(axis.text.x = element_text(angle = 45, vjust = 1, hjust = 1),
        axis.title.x = element_blank()) + ylab("rLog transformed expression value")
```

##样本层级聚类

```{r}
print("Performing sample clustering")
hmcol <- colorRampPalette(brewer.pal(9, "GnBu"))(100)
pearson_cor <- round(as.matrix(cor(rlogMat, method="pearson")),4)

hc <- hcluster(t(rlogMat), method="pearson")

# Get lower triangle of the correlation matrix
get_lower_tri<-function(cormat){
	cormat[upper.tri(cormat)] <- NA
	return(cormat)
}
# Get upper triangle of the correlation matrix
get_upper_tri <- function(cormat){
	cormat[lower.tri(cormat)]<- NA
	return(cormat)
}

pearson_cor <- pearson_cor[hc$order, hc$order]

pearson_cor_output = data.frame(id=rownames(pearson_cor), pearson_cor)
write.table(pearson_cor_output, file=paste0(ehbio_output_prefix,".DESeq2.pearson_cor.xls"),
quote=F, sep="\t", row.names=F, col.names=T)

upper_tri <- get_upper_tri(pearson_cor)
# Melt the correlation matrix
melted_cormat <- melt(upper_tri, na.rm = TRUE)

col = colorRampPalette(rev(brewer.pal(n=7, name="RdYlBu")))(100)

# Create a ggheatmap
p <- ggplot(melted_cormat, aes(Var2, Var1, fill = value))+
 geom_tile(color = "white")+
 scale_fill_gradientn(colours=col, name="Pearson correlation") + theme_classic() +
  coord_fixed() + 
 theme(
  axis.text.x = element_text(angle = 45, vjust = 1, hjust = 1),
  axis.title.x = element_blank(),
  axis.title.y = element_blank(),
  legend.justification = c(1, 0),
  legend.position = "top",
  legend.direction = "horizontal")+
  guides(fill = guide_colorbar(barwidth = 8, barheight = 1,
                title.position = "left"))

p
ggsave(filename=paste0(ehbio_output_prefix,".DESeq2.normalized.rlog.pearson.pdf"),width=13.5,height=15,units=c("cm"))
```

##PCA聚类分析


```{r pca}
#print("PCA analysis")
formulaV <- c("conditions")

topn = 5000
rlogMat_nrow = nrow(rlogMat)
if (topn > rlogMat_nrow){
  topn = rlogMat_nrow
}

pca_mat = rlogMat[1:topn,]
pca_mat <- as.data.frame(t(pca_mat))

pca <- prcomp(pca_mat, scale=T)

pca_x = pca$x

pca_individual = data.frame(samp=rownames(pca_x), pca_x, sample)

write.table(pca_individual, file=paste0(ehbio_output_prefix,".DESeq2.pca_individuals.xls"), sep="\t", quote=F, row.names=F, col.names=T)

pca_percentvar <- formatC(pca$sdev^2 * 100 / sum( pca$sdev^2))


if (length(formulaV)==1) {
  p <- ggplot(pca_individual, aes(PC1, PC2, color=conditions))
} else if (length(formulaV==2)) {
  p <- ggplot(pca_data, aes(PC1, PC2, color=conditions,
  shape=conditions))
}

p = p + geom_point(size=3) + 
	xlab(paste0("PC1: ", pca_percentvar[1], "% variance")) +
	ylab(paste0("PC2: ", pca_percentvar[2], "% variance")) +
	geom_text_repel(aes(label=samp), show.legend=F) +
	theme_classic() +
	theme(legend.position="top", legend.title=element_blank())

p
ggsave(p, filename=paste0(ehbio_output_prefix,".DESeq2.normalized.rlog.pca.pdf"),width=13.5,height=15,units=c("cm"))

pca_percentvar <- data.frame(PC=colnames(pca_x), Variance=pca_percentvar)
write.table(pca_percentvar, file=paste0(ehbio_output_prefix,".DESeq2.pca_pc_weights.xls"), sep="\t", quote=F, row.names=F, col.names=T)
```

##两组样品基因差异分析

```{r, de_twosample}

if (file.exists(paste0(ehbio_output_prefix,".DESeq2.all.DE"))) file.remove(paste0(ehbio_output_prefix,".DESeq2.all.DE"))

# 定义待比较的两个样本的分组名字
sampleA <- "untrt"
sampleB <- "trt"

# 后面无需修改
print(paste("DE genes between", sampleA, sampleB, sep=" "))
contrastV <- c("conditions", sampleA, sampleB)
res <- results(dds,  contrast=contrastV)
baseA <- counts(dds, normalized=TRUE)[, colData(dds)$conditions == sampleA]
if (is.vector(baseA)){
  baseMeanA <- as.data.frame(baseA)
} else {
  baseMeanA <- as.data.frame(rowMeans(baseA))
}
baseMeanA <- round(baseMeanA, 3)
colnames(baseMeanA) <- sampleA
baseB <- counts(dds, normalized=TRUE)[, colData(dds)$conditions == sampleB]
if (is.vector(baseB)){
  baseMeanB <- as.data.frame(baseB)
} else {
  baseMeanB <- as.data.frame(rowMeans(baseB))
}
baseMeanB <- round(baseMeanB, 3)
colnames(baseMeanB) <- sampleB
res <- cbind(baseMeanA, baseMeanB, as.data.frame(res))
res <- data.frame(ID=rownames(res), res)
res$baseMean <- round(rowMeans(cbind(baseA, baseB)),3)
res$padj[is.na(res$padj)] <- 1
res$pvalue[is.na(res$pvalue)] <- 1
res$log2FoldChange <- round(res$log2FoldChange,3)
res$padj <- as.numeric(formatC(res$padj))
res$pvalue <- as.numeric(formatC(res$pvalue))

res <- res[order(res$padj),]

comp314 <- paste(sampleA, "_vs_", sampleB, sep=".")

file_base <- paste(ehbio_output_prefix, ".DESeq2", comp314, sep=".")
file_base1 <- paste(file_base, "results.xls", sep=".")

res_output <- as.data.frame(subset(res,select=c('ID',sampleA,sampleB,"baseMean",'log2FoldChange','pvalue', 'padj')))
write.table(res_output, file=file_base1, sep="\t", quote=F, row.names=F)

res_de <- subset(res, res$padj<0.05, select=c('ID', sampleA,
                                              sampleB, 'log2FoldChange', 'padj'))
res_de_up <- subset(res_de, res_de$log2FoldChange>=1)
file <- paste(ehbio_output_prefix, ".DESeq2",sampleA, "_higherThan_", sampleB, 'xls', sep=".") 
write.table(as.data.frame(res_de_up), file=file, sep="\t", quote=F, row.names=F)
res_de_up_id <- subset(res_de_up, select=c("ID"))
#file <- paste(file_base, "DE_up_id", sep=".")
file <- paste(ehbio_output_prefix, ".DESeq2",sampleA, "_higherThan_", sampleB,'id.xls', sep=".") 
write.table(as.data.frame(res_de_up_id), file=file, sep="\t", 
            quote=F, row.names=F, col.names=F)

if(dim(res_de_up_id)[1]>0) {
  res_de_up_id_l <- cbind(res_de_up_id, paste(sampleA, "_higherThan_",sampleB, sep="."))
  write.table(as.data.frame(res_de_up_id_l), file=paste0(ehbio_output_prefix,".DESeq2.all.DE"),
              sep="\t",quote=F, row.names=F, col.names=F, append=T)
}

res_de_dw <- subset(res_de, res_de$log2FoldChange<=(-1)*1)
file <- paste(ehbio_output_prefix, ".DESeq2",sampleA, "_lowerThan_", sampleB, 'xls', sep=".") 
write.table(as.data.frame(res_de_dw), file=file, sep="\t", quote=F, row.names=F)
res_de_dw_id <- subset(res_de_dw, select=c("ID"))
file <- paste(ehbio_output_prefix, ".DESeq2",sampleA, "_lowerThan_", sampleB, 'id.xls', sep=".") 
write.table(as.data.frame(res_de_dw_id), file=file, sep="\t", 
            quote=F, row.names=F, col.names=F)

if(dim(res_de_dw_id)[1]>0) {
  res_de_dw_id_l <- cbind(res_de_dw_id, paste(sampleA, "_lowerThan_",sampleB, sep="."))
  write.table(as.data.frame(res_de_dw_id_l), file=paste0(ehbio_output_prefix,".DESeq2.all.DE"),
              sep="\t",quote=F, row.names=F, col.names=F, append=T)
}

res_output$level <- ifelse(res_output$padj<=0.05, ifelse(res_output$log2FoldChange>=1, paste(sampleA,"UP"), ifelse(res_output$log2FoldChange<=1*(-1), paste(sampleB,"UP"), "NoDiff")) , "NoDiff")
res_output$padj <- (-1) * log10(res_output$padj)
res_output$padj <- replace(res_output$pad, res_output$pad>5, 5.005)

boundary = ceiling(max(abs(res_output$log2FoldChange)))
p = ggplot(res_output, aes(x=log2FoldChange,y=padj,color=level)) +
  #geom_point(aes(size=baseMean), alpha=0.5) + theme_classic() +
  geom_point(size=1, alpha=0.5) + theme_classic() +
  xlab("Log2 transformed fold change") + ylab("Negative Log10 transformed FDR") +
  xlim(-1 * boundary, boundary) + theme(legend.position="top", legend.title=element_blank())
ggsave(p, filename=paste0(file_base1,".volcano.pdf"),width=13.5,height=15,units=c("cm"))
p

```
##根据log2FolcChange排序基因

```{r}
#head(res_output)
# 整理数据，按差异倍数排序，增加横轴，选择log2差异倍数大于5的标记基因名字
res_output_line <- res_output[order(res_output$log2FoldChange),]
res_output_line$x <- 1:nrow(res_output_line)
res_output_line[abs(res_output_line$log2FoldChange)<5 | res_output_line$level=="NoDiff", "ID"] <- NA
head(res_output_line)

library(ggrepel)
p <- ggplot(res_output_line, aes(x=x, y=log2FoldChange)) + geom_point(aes(color=log2FoldChange)) + 
  scale_color_gradient2(low="dark green", mid="yellow", high= "dark red", midpoint = 0) + 
  theme_classic() + geom_hline(yintercept = 0, linetype="dotted")
p

# 标记基因名字
p +  geom_text_repel(aes(label=ID))
```

##Top20差异显著的基因

```{r}
res_de_up_top20_id <- as.vector(head(res_de_up$ID,20))
res_de_dw_top20_id <- as.vector(head(res_de_dw$ID,20))

res_de_top20 <- c(res_de_up_top20_id, res_de_dw_top20_id)
res_de_top20
```

#差异基因热图

```{r, fig.height=8}
# 可以把矩阵存储，提交到www.ehbio.com/ImageGP绘制火山图
# 或者使用我们的s-plot https://github.com/Tong-Chen/s-plot
res_de_top20_expr <- normalized_counts[res_de_top20,]
res_de_top20_expr
library(pheatmap)
pheatmap(res_de_top20_expr, cluster_row=T, scale="row", annotation_col=sample)
```

#差异基因散点图

```{r, fig.width=10}
# 增加基因名字列
res_de_top20_expr2 <- data.frame(Gene=rownames(res_de_top20_expr), res_de_top20_expr)
head(res_de_top20_expr2)

# 转换为长格式
res_de_top20_expr2 <- melt(res_de_top20_expr, id=c("Gene"))
colnames(res_de_top20_expr2) <- c("Gene", "Sample", "Expression")
head(res_de_top20_expr2)

# 图形绘制
ggplot(res_de_top20_expr2, aes(x=Gene, y=Expression)) + geom_point(aes(color=Sample), alpha=0.5) + theme_classic() +
  theme(axis.text.x = element_text(angle = 45, vjust = 1, hjust = 1),
        axis.title.x = element_blank()) + ylab("Normalized xpression value") + scale_y_log10()
```

差异基因散点图

```{r, fig.width=10}
# 增加分组信息属性
res_de_top20_expr2$Group <- sample[match(res_de_top20_expr2$Sample, rownames(sample)),1]
head(res_de_top20_expr2)

# 图形绘制
ggplot(res_de_top20_expr2, aes(x=Gene, y=Expression)) + geom_point(aes(color=Group), alpha=0.5) + theme_classic() +
  theme(axis.text.x = element_text(angle = 45, vjust = 1, hjust = 1),
        axis.title.x = element_blank()) + ylab("Normalized xpression value") + scale_y_log10()
```
```{r}
head(res_de_top20_expr2)
```
##多组样品两两差异分析

定义样品两两比较函数

```{r, de_twosample}
de_twosample <- function
(
dds, 
sampleV
){
	#print(sampleV)
	sampleA <- as.vector(sampleV$sampA)
	sampleB <- as.vector(sampleV$sampB)
	print(paste("DE genes between", sampleA, sampleB, sep=" "))
	contrastV <- c("conditions", sampleA, sampleB)
	res <- results(dds,  contrast=contrastV)
	baseA <- counts(dds, normalized=TRUE)[, colData(dds)$conditions == sampleA]
	if (is.vector(baseA)){
		baseMeanA <- as.data.frame(baseA)
	} else {
		baseMeanA <- as.data.frame(rowMeans(baseA))
	}
	baseMeanA <- round(baseMeanA, 3)
	colnames(baseMeanA) <- sampleA
	baseB <- counts(dds, normalized=TRUE)[, colData(dds)$conditions == sampleB]
	if (is.vector(baseB)){
		baseMeanB <- as.data.frame(baseB)
	} else {
		baseMeanB <- as.data.frame(rowMeans(baseB))
	}
	baseMeanB <- round(baseMeanB, 3)
	colnames(baseMeanB) <- sampleB
	res <- cbind(baseMeanA, baseMeanB, as.data.frame(res))
	res <- data.frame(ID=rownames(res), res)
	res$baseMean <- round(rowMeans(cbind(baseA, baseB)),3)
	res$padj[is.na(res$padj)] <- 1
	res$pvalue[is.na(res$pvalue)] <- 1
	res$log2FoldChange <- round(res$log2FoldChange,3)
	res$padj <- as.numeric(formatC(res$padj))
	res$pvalue <- as.numeric(formatC(res$pvalue))

	res <- res[order(res$padj),]

	comp314 <- paste(sampleA, "_vs_", sampleB, sep=".")

	file_base <- paste(ehbio_output_prefix, ".DESeq2", comp314, sep=".")
	file_base1 <- paste(file_base, "results.xls", sep=".")

	res_output <- as.data.frame(subset(res,select=c('ID',sampleA,sampleB,"baseMean",'log2FoldChange','pvalue', 'padj')))
	write.table(res_output, file=file_base1, sep="\t", quote=F, row.names=F)
	
	res_de <- subset(res, res$padj<0.05, select=c('ID', sampleA,
		sampleB, 'log2FoldChange', 'padj'))
	res_de_up <- subset(res_de, res_de$log2FoldChange>=1)
	file <- paste(ehbio_output_prefix, ".DESeq2",sampleA, "_higherThan_", sampleB, 'xls', sep=".") 
	write.table(as.data.frame(res_de_up), file=file, sep="\t", quote=F, row.names=F)
	res_de_up_id <- subset(res_de_up, select=c("ID"))
	#file <- paste(file_base, "DE_up_id", sep=".")
	file <- paste(ehbio_output_prefix, ".DESeq2",sampleA, "_higherThan_", sampleB,'id.xls', sep=".") 
	write.table(as.data.frame(res_de_up_id), file=file, sep="\t", 
		quote=F, row.names=F, col.names=F)
	
	if(dim(res_de_up_id)[1]>0) {
		res_de_up_id_l <- cbind(res_de_up_id, paste(sampleA, "_higherThan_",sampleB, sep="."))
		write.table(as.data.frame(res_de_up_id_l), file=paste0(ehbio_output_prefix,".DESeq2.all.DE"),
		sep="\t",quote=F, row.names=F, col.names=F, append=T)
	}
		
	res_de_dw <- subset(res_de, res_de$log2FoldChange<=(-1)*1)
	file <- paste(ehbio_output_prefix, ".DESeq2",sampleA, "_lowerThan_", sampleB, 'xls', sep=".") 
	write.table(as.data.frame(res_de_dw), file=file, sep="\t", quote=F, row.names=F)
	res_de_dw_id <- subset(res_de_dw, select=c("ID"))
	file <- paste(ehbio_output_prefix, ".DESeq2",sampleA, "_lowerThan_", sampleB, 'id.xls', sep=".") 
	write.table(as.data.frame(res_de_dw_id), file=file, sep="\t", 
		quote=F, row.names=F, col.names=F)

	if(dim(res_de_dw_id)[1]>0) {
		res_de_dw_id_l <- cbind(res_de_dw_id, paste(sampleA, "_lowerThan_",sampleB, sep="."))
		write.table(as.data.frame(res_de_dw_id_l), file=paste0(ehbio_output_prefix,".DESeq2.all.DE"),
		sep="\t",quote=F, row.names=F, col.names=F, append=T)
	}

	res_output$level <- ifelse(res_output$padj<=0.05, ifelse(res_output$log2FoldChange>=1, paste(sampleA,"UP"), ifelse(res_output$log2FoldChange<=1*(-1), paste(sampleB,"UP"), "NoDiff")) , "NoDiff")
	res_output$padj <- (-1) * log10(res_output$padj)
	res_output$padj <- replace(res_output$pad, res_output$pad>5, 5.005)
	
	boundary = ceiling(max(abs(res_output$log2FoldChange)))
	p = ggplot(res_output, aes(x=log2FoldChange,y=padj,color=level)) +
         #geom_point(aes(size=baseMean), alpha=0.5) + theme_classic() +
         geom_point(size=1, alpha=0.5) + theme_classic() +
	 	 xlab("Log2 transformed fold change") + ylab("Negative Log10 transformed FDR") +
		 xlim(-1 * boundary, boundary) + theme(legend.position="top", legend.title=element_blank())
	ggsave(p, filename=paste0(file_base1,".volcano.pdf"),width=13.5,height=15,units=c("cm"))
	p
}
```

样品分组组合，并调用函数

```{r}
if (file.exists(paste0(ehbio_output_prefix,".DESeq2.all.DE"))) file.remove(paste0(ehbio_output_prefix,".DESeq2.all.DE"))

compare_data <- as.vector(unique(sample$conditions))

len_compare_data <- length(compare_data)
for(i in 1:(len_compare_data-1)) {
  for(j in (i+1):len_compare_data) {
    tmp_compare <- data.frame(sampA=compare_data[i],sampB=compare_data[j])
    de_twosample(dds, tmp_compare)
  }
}
```





##结果文件描述

```
# 具体的文件内容和图的样式见后面的分步法文档
# 原始输入文件
salmon.output
sampleFile

# 所有差异基因列表
ehbio_trans.Count_matrix.xls.DESeq2.all.DE

# PCA结果
ehbio_trans.Count_matrix.xls.DESeq2.normalized.rlog.pca.pdf

# 样品相关性层级聚类结果
ehbio_trans.Count_matrix.xls.DESeq2.normalized.rlog.pearson.pdf

# rlog转换后的标准化后的表达结果
ehbio_trans.Count_matrix.xls.DESeq2.normalized.rlog.xls

# 标准化后的表达结果
ehbio_trans.Count_matrix.xls.DESeq2.normalized.xls

# 运行脚本
ehbio_trans.Count_matrix.xls.DESeq2.r

# 差异基因结果
ehbio_trans.Count_matrix.xls.DESeq2.untrt._higherThan_.trt.id.xls
ehbio_trans.Count_matrix.xls.DESeq2.untrt._higherThan_.trt.xls
ehbio_trans.Count_matrix.xls.DESeq2.untrt._lowerThan_.trt.id.xls
ehbio_trans.Count_matrix.xls.DESeq2.untrt._lowerThan_.trt.xls

# 火山图和火山图输入数据
ehbio_trans.Count_matrix.xls.DESeq2.untrt._vs_.trt.results.xls
ehbio_trans.Count_matrix.xls.DESeq2.untrt._vs_.trt.results.xls.volcano.pdf
```

##转换基因表的ENSEM id为gene symbol (为GSEA准备)

```{bash}
cd /c/transcriptome/13_salmon_deseq2_go
awk 'BEGIN{OFS=FS="\t"}ARGIND==1{ensg2sym[$1]=$2;}ARGIND==2{if(FNR==1) print $0; else {a=ensg2sym[$1]; if(a!="") {$1=a; print $0;}}}' genome/GRCh38.idmap ehbio_salmon.DESeq2.normalized.xls >ehbio_salmon.DESeq2.normalized.symbol.txt

head ehbio_salmon.DESeq2.normalized.symbol.txt
```

##提取Log2FC值并转换为gene symbol (为GSEA准备)

```{r}
suppressMessages(library(data.table))

vs_result <- read.table("ehbio_salmon..DESeq2.untrt._vs_.trt.results.xls", header=T, sep="\t", quote="")

vs_result <- subset(vs_result, select=c("ID","log2FoldChange"))

vs_result <- data.table(vs_result, key="ID")

idmap <- read.table("genome/GRCh38.idmap", header=T, sep="\t", quote="")
idmap <- data.table(idmap, key="ENSG")

merge_result <- merge(vs_result, idmap, by.x="ID", by.y="ENSG", all.x=T)

merge_result <- merge_result[order(merge_result$log2FoldChange, decreasing = T),]

merge_result <- merge_result[merge_result$Symbol!="", c(3,2)]

write.table(merge_result, "ehbio_salmon.DESeq2.log2fc_ranked.symbol", col.names = T, row.names = F, sep="\t", quote=F)
```

##转换所有差异基因的名字为gene symbol 或 entrez id (为GO富集分析准备)

```{bash}
# GRCh38.idmap从ENSEMBL Biomart下载，三列文件，第一列为ensembl ID，第二列为gene symbol, 第三列为entrez id
awk 'BEGIN{OFS=FS="\t"}ARGIND==1{entrez[$1]=$3;}\
	ARGIND==2{if(entrez[$1]!="") print entrez[$1],$2;}' \
	genome/GRCh38.idmap ehbio_salmon.DESeq2.all.DE \
	>ehbio.DESeq2.all.DE.entrez
awk 'BEGIN{OFS=FS="\t"}ARGIND==1{symbol[$1]=$2;}\
	ARGIND==2{if(symbol[$1]!="") print symbol[$1],$2;}' \
	genome/GRCh38.idmap ehbio_salmon.DESeq2.all.DE \
	>ehbio.DESeq2.all.DE.symbol
```

##DEseq2分步计算

```
if ("" != "") {
	print("Using given sizeFactor")
	sizeFactorGiven = read.table("", header=T, row.names=1, 
		sep="\t")
	sizeFactorGiven2 = as.vector(unlist(sizeFactorGiven))
	names(sizeFactorGiven2) = rownames(sizeFactorGiven)
	sizeFactorGiven = sizeFactorGiven2
	sizeFactors(dds) <- sizeFactorGiven
} else {
	print("estimate sizeFactor")
	dds <- estimateSizeFactors(dds)
	sizeFactorGenerate = sizeFactors(dds)	
	write.table(sizeFactorGenerate, "./Public/ehbio/tmp/Monocyte_HSC_exprmat.txt.DESeq2.sizeFactor.xls", sep="\t", 
		quote=F, row.names=T, col.names=T)
}

dds <- estimateDispersions(dds)
dds <- nbinomWaldTest(dds)
```
#至此，salmon. DESeq2. Rmd已结束
