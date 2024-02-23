# my-rnaseq
争取早日成为生信高手
# Linux操作基础
```
orkj3401772k2ei3
0heyuanyu@

**home光标回到开头
clear清屏
gzip -d Triticum_aestivum.IWGSC.58.gtf.gz 解压文件

 free -h查看服务器内存
top 查看进程及使用内存

ls列出目录内容
ls 命令用来列出目录内容
相关选项:
 ls –a  显示所有文件(包括隐藏文件)
 ls –l  显示详细信息  缩写为ll
 ls –t  时间顺序显示文件
    ls –l  地址 查看特定地址目录
应用
 不离开当前路径查看其他文件或者进入其他目录
 用路径指向数据文件，告诉命令或者软件我要处理分析那个数据
 判断目录或者文件是否存在？
 解决报错： No such file or directory ,通过ll和cd检查

cd切换路径
  cd 切换目录
 上一级目录 ”..”
 当前目录   ”.”
 用户家目录 ” ~”
 上一个工作目录 ” -”
 空  回到家目录
 cd    目录

Linux文件系统目录结构
 Linux文件系统为一个倒转的单根树状结构
 Linux文件系统的根为 ”/ ”
 Linux文件系统严格区分大小写 （tmp Tmp）
 目录路径使用 ”/ ” 分割        (Windows中使用” \ ”)
 Linux目录路径表示：  /var/log/samba
 Windows目录路径表示：  C:\Users\Administrator

当前工作目录
 打开一个终端自动进入用户的家目录
 pwd命令可以显示当前的工作目录
 每一个终端都有一个当前工作目录

绝对路径和相对路径
 路径：可以指向一个文件或者目录
 绝对路径:以 ”/ ”开头，递归每级目录直到目标的路径，目录
之间用”/”分隔
不受当前所在工作目录的影响
 相对路径:以当前目录为起点，指向一个文件或者目录
受当前所在目录影响
 绝对路径:/var/log/samba
 相对路径:../../var/log/samba

BASH-命令补齐
 使用Tab键来简化命令输入
 自动补全命令
 自动补全文件名
 例如：
 $ hmms<tab>
 $ ls Downl<tab>
 $ ls Downloads

BASH-历史记录
 Bash会记录你输入的命令
可以通过上下按键或者history命令查看历史记录
 通过history命令查看历史记录 ，也可以跟参数-1000，指定打印行数
 通过：! 匹配运行历史记录 ，如:!salmo,则将运行记录中最近的以salmo开头的指令

 Bash Shell支持以下通配符:
    *
    匹配零个或多个（重点掌握）例如：ll *fa显示所有已fa结尾的文件。ll hekun*显示所有已hekun开头的文件
    ?
    匹配任意一个字符。例如：ll rnaseq_?.fa显示所有fa。其中问号只代表一个字符的文件。ll rnaseq_??.fa显示所有fa。其中两个问号代表两个字符的文件
    []
    匹配列举的一个字符，如下
    [0-9]
    匹配一个数字范围
    [abc]
    匹配列表里（即a或b或c）任意字符
    [^abc]匹配列表（即a或b或c）以外字符

BASH任务管理
 在后台运行命令
在命令后添加一个 &
 暂停或停止某个程序
Ctrl+z（暂停) Ctrl+c（停止）
 管理后台任务
jobs(查看当前所有后台任务)
bg(控制进程继续在后台执行)  %1
fg(将后台任务拉回前台)  %1
kill(将任务杀死)  %1
nohup sh wget.sh >wget.sh.o&
&转后台，但是关掉服务器会暂停，加上nohup之后，就不会暂停了，>wget.sh.o是指将本该出现在屏幕上的日志重定向输出到一个新的文件wget.sh.o

切换用户（选修）
 在CLI中,通过su命令切换用户
su    切换到root用户但不使用新的运行环境
su -  切换到root用户并使用一个新的运行环境
sudo  使用管理员用户身份运行命令
 修改当前用户密码  passwd
exit 退出当前用户

创建、删除文件
 touch  命令可以创建一个空文件或更新文件
 rm  命令可以删除文件(使用时需十分谨慎)
 mkdir 命令创建一个目录
 rm –r (-f) 命令删除一个非空目录
-r 递归的删除包括目录中的所有内容
-f 强制删除，没有警告提示 (使用时需十分谨慎)

cp复制文件、目录
 使用cp命令复制文件或目录
 cp 源文件(目录) 目标文件(目录)
 常见选项:
-r  递归复制整个目录树
-v  显示详细信息(显示复制过程)

mv移动、重命名文件或目录
 文件的名称大小写敏感
 名称最多可以为255个字符
 除了“/”正斜线外，都是有效字符(建议用[A-Za-z0-9]_)
 通过mv命令移动或者重命名文件或目录
 mv 文件 目标目录
 如果指定文件名，则可以重命名文件


文件权限
- 所有者  usr
- 所在组  group
- 其它组  other
r=读，w=写，x=执行

chmod 改变文件或目录的权限（选修）
 字母形式
 r=读，w=写，x=执行
 chmod u=rwx，g=rx，o=rx  abc   ：同上u=用户权限，g=组权限，o=不同组其他用户权限
 chmod u-x，g+w abc   ：给abc去除用户执行的权限，增加组写的权限
 chmod a+r abc     ：给所有用户添加读的权限
 数字形式
 r=4，w=2，x=1
若要rwx属性则4+2+1=7；
若要rw-属性则4+2=6；
若要r-x属性则4+1=5。
 chmod 755 abc：赋予abc权限rwxr-xr-x

输出、查看命令
 cat用以显示文件内容 zcat 打开压缩文件
 head用以显示文件的头几行(默认10行) -n  指定显示的行数
 tail用以显示文件的末尾几行(默认10行) -n  指定显示的行数
 more用于翻页显示文件内容(只能向下翻页) ，按q退出
 less用于翻页显示文件内容(带上下翻页)  -S 不换行（更整洁工整）  -N 加行号，二者可以直接写成-SN ，按q退出。less中/表示搜索，例如：/gene，即表示搜索文件中的gene字符，按n下一个。按上下键可查看指令记录
 wc –l  统计行数

grep命令搜索筛选
 用于过滤/搜索特定字符
 多种命令配合使用，使用上十分灵活
-c    --count   #计算符合样式的列数。
grep -c "<" Arabidopsis thaliana.TAIR10.pep.all.fa。
-v   --revert-match   #显示不包含匹配文本的所有行。
-i  忽略大小写
grep -i "MYB' Arabidopsis thaliana.TAIR10.pep.all.fa。在文件中搜索myb（不区分大小写），其中myb是一种总转录因子，也可以改为mads等
grep -i "MYB' Arabidopsis thaliana.TAIR10.pep.all.fa >myb.txt。将结果重定向到文件保存

cut 按列分隔文件
 cut -f 2 -d";" test.test.gff3 （分隔符可以使任何字符，根据文件确定，比如空格）
    cut -f 2,4,6 -d";" test.test.gff3 提取多行（分隔符可以使任何字符，根据文件确定，比如空格）
    cut -f 1-6 -d";" test.test.gff3 提取多行（分隔符可以使任何字符，根据文件确定，比如空格）
-f  指定显示哪一列 cut -f 2  test.gff3提取文件的第二列（没指认分隔符则默认TAB）
-d  指定分隔符号，默认的字段分隔符为“TAB”
也可以不用-d参数，而是用-c参数，提取特定字符。cut -c 2-10 -d";" test.test.gff3(提取每行第二至第十个字符)
cut -c 2-10 -d";" test.test.gff3 >gene_id.txt(提取每行第二至第十个字符并保存)

查找
 命令find用以高级查找文件、目录
 find 查找位置 查找参数 可以跟绝对和相对路径
 如:
 find . / 会搜索显示当前文件夹所有文件，
 find . –name *fastq* 搜索含有fastq的文件
 find / -name *.conf  搜索以.conf结尾的文件
 find . –name “*fa” –exec ls –l {} \; （对搜索的fa文件进行批量处理）
 find . –name “*fa” –exec grep –c ">" {} \; （对搜索的fa文件进行批量处理,处理的命令为grep –c ">"）

获取帮助
 man命令
-h  --help
 Linux命令大全：http://man.linuxde.net/

VIM/VI
 绝大多数Linux系统上均安装有vim，vim比vi的功能更为强大，所以建议大
家使用vim而非vi，两者使用方法相同。
 vim   目标文件路径
 如果目标文件存在，则vim打开该文件。
 如果目标文件不存在，则vim新建并打开该文件。

VIM模式
vim拥有三种模式:
-命令模式(常规模式)
vim启动后，默认进入命令模式，任何模式都可以通过按esc键回到命令模式(可以多
按几次)。命令模式下可以通过键入不同的命令完成选择、复制、粘贴、撤销等等操作。
-插入模式
在命令模式中按”i”键，即可进入插入模式，在插入模式可以输入编辑文本内容，
使用esc键可以返回命令模式。
-ex模式
在命令模式中按”:”键可以进入ex模式，光标会移动到底部，在这里可以保存修改
或退出vim。 该模式下:set number设置行号，w保存，q退出

命令模式
 Vim启动后，默认进入命令模式，任何模式都可以通过按esc键进入命令模式(可
以多按几次)。命令模式常用命令如下:
 i     在光标前插入文本   a 光标后插入文本（切换到插入模式）
 o     在当前行的下面插入新行
 dd    删除整行
 yy    将当前行的内容放入缓冲区(复制当前行)
 n+yy  将n行的内容放入缓冲区(复制n行)
    p    将缓冲区中的文本放入光标后(粘贴)
 u     撤销上一个操作
 r     替换当前字符
 /     查找关键字。如/perl即在文本中搜索并定位perl


EX模式
 在命令模式中按”:”键可以进入ex模式，光标会移动到底部，在这里可以保
存修改或退出vim。Ex模式下常用命令如下:
:w
:q
保存当前修改
退出
:wq  保存退出    快捷键 ZZ
:q! 强制退出，不保存修改
:x
保存并退出，相当于:wq
:set number 显示显示行号
:%s/id/myid/ 在全文本中搜索id并替换所有行第一个id为myid，%代表全局，s搜索
:%s/id/myid/g在全文本中搜索id并替换所有id为myid
:2,20%s/id/myid/g在第2至第22行中搜索id并替换所有id为myid，g代表全局

插入模式
 在命令模式中按”i”键，即可进入插入模式，在插入模式可以输
入编辑文本内容，使用esc键可以返回命令模式。


sed搜索替换文件内容 ，支持正则表达式
 sed用法：
 sed [选项] ‘command’ 输入文件
 搜索举例：sed ‘s/Myb/Gene/’file.txt    s搜索，搜索每行第一个Myb，更改为Gene，///也可以换位###
sed ‘s/Myb/Gene/gi’file.txt | less -SN       s搜索，g全局，i忽略，搜索所有Myb不论大小写，都更改为Gene，|管道，将输出结果传递到下一个指令
sed ‘s/.*Myb/Gene/gi’file.txt | less -SN      s搜索，g全局，i忽略，搜索所有Myb不论大小写，.代表任意一个字符，*代表0或多个其前方的特定字符。搜索myb，无论前面有几个任意字符，直接替换为Gene
 直接修改文件内容(危险动作，不像vim可以撤回)
-i  选项
在前面操作确认无误后，再将-i加上
sed -i ‘s/Myb//g’file.txt ，直接保存修改
sed -i.bak‘s/Myb//g’file.txt ，保存修改前备份文件并以.bak结尾

删除某行
sed '1d 'file.txt      #删除第一行
sed '$d' file.txt      #删除最后一行
sed '1,2d' file.txt    #删除第一行到第二行
sed '2,$d' file.txt     #删除第二行到最后一行

显示某行
p命令（打印匹配行）
如果加上-n参数后，则只有经过sed特殊处理的那一行（或者动作）才会被列出来,如果不加n，则会打印指定行以及所有行
sed -n '1p' file.txt
#显示第一行
sed -n '$p' file.txt
#显示最后一行
sed -n '1,2p' file.txt
#显示第一行到第二行
sed -n' 2,$p' file.txt
#显示第二行到最后一行
sed -n '/MYB/p'ab
#查询包括关键字MYB所在所有行（类似grep功能）

管道 |  叠加使用命令
 所有能打印到屏幕（标准输出）的内容都可以通过管道传递给下
一个命令（前提条件是下一个命令可以接收标准输入）.
 ls | grep “manager”
 grep
 cat
 zcat
 …

屏幕输出到新文件 >
 标准输出到文件 ：
 新建 >
 追加 >>

命令举例
cat打开打印文件效率比less高
    cat Arabidopsis_thaliana. TAIR10. pep. all. fa |grep '>' > fasta. id. txt     ，将文件中带有>的行保存为fasta. id. txt
 cat fasta. id. txt |grep -i‘MYB’|cut –f 1 –d  “ ” |less –SN         提取文件fasta. id. txt中含有myb的所有行，忽略大小写，并提取第一列以空格分列，并使用less打开
 cat fasta. id. txt |grep -i‘MYB’|cut –f 1 –d  “ ” |sed 's/>//'  |sed 's/\.[0-9]*//'|less –SN        提取文件fasta. id. txt中含有myb的所有行，忽略大小写，并提取第一列以空格分列（格式为>AT5G06800.1），接下来删除>,然后删除.以及以后的数字因为.只是想表达为普通的小数点，所以使用了转义符\，而且后面的数字也可能是多位数，所以加了*,，  并使用less打开
 cat fasta. id. txt |grep -i‘MYB’|cut –f 1 –d  “ ” |sed 's/>//'  |sed 's/\.[0-9]*//' >myb_id
        提取文件fasta. id. txt中含有myb的所有行，忽略大小写，并提取第一列以空格分列（格式为>AT5G06800.1），接下来删除>,然后删除.以及以后的数字因为.只是想表达为普通的小数点，所以使用了转义符\，而且后面的数字也可能是多位数，所以加了*,，  确认无误后保存文件
 cat fasta. id. txt |grep -i‘MYB’|wc  -l


awk命令基本用法
 awk [选项] ‘BEGIN{} {command1; command2} END{}’ file

AWK内置特殊变量
属性 说明
$0 当前记录（作为单个变量）
$1~$n 当前记录的第n个字段，字段间由FS分隔
FS 输入字段分隔符 默认是空格
NF 当前记录中的字段个数，就是有多少列
NR 已经读出的记录数，就是行号，从1开始
RS 输入的记录他隔符默 认为换行符
OFS 输出字段分隔符 默认也是空格
ORS 输出的记录分隔符，默认为换行符

awk命令筛选分割数据
 默认用空白（TAb和空格）分隔数据列，指定分隔符用-F参数

awk命令筛选分割数据
 awk  ’{if ($3==“gene”) print $0}’ Arabidopsis_thaliana.TAIR10.41.gff3       可以简写为   awk ‘$3==“gene” {print $0}’ Arabidopsis_thaliana.TAIR10.41.gff3
 awk  ’{if ($1 != “1“ ) print $0}’ Arabidopsis_thaliana.TAIR10.41.gff3 ，!取反，第一列不等于1
 awk  -F “[;=\t]" ‘{ print $1  }’Arabidopsis_thaliana.TAIR10.41.gff3
 AND 与关系: awk ’{if ( $1==“1” && $3==“gene” ) print $0}’Arabidopsis_thaliana.TAIR10.41.gff3 ，同时满足
 OR 或关系: awk ’{if ($1==“1" || $1==“2”) print $0}’Arabidopsis_thaliana.TAIR10.41.gff3，满足其一即可

 grep -v ‘#’ Arabidopsis_thaliana.TAIR10.41.gff3 |awk  ’{if ($3==“gene”) print }’ |awk -F "[\t;=]"
‘{print $1,$4,$5,$10}’|less -SN
输出不包含#数据的行传递给awk，输出第三列为gene的行，将输出以[\t;=四种做分隔符分成多列，并输出1,4,5,10列，传递给less查看
awk -F "[\t=;:]" ' BEGIN{OFS="\t"} $3=="gene" && NR >1000 { print NR,$11,$1,$4,$5,$7}' Arabidopsis_thaliana. TAIR10.41. gff3 |less -SN
以\t=;:做分隔符将文件分割为多列，以\t做分隔符输出结果，&&同时满足，NR表示该行数据在原文件中的行号
awk -F "\t"'BEGIN{ IGNORECASE=1; OFS=\t"} $3==gene"&& $9~/NAC/{ print $1,$4,$5,$7,$9}' Arabidopsis_thaliana. TAIR10.41. gff3 |less -SN
IGNORECASE=1是指忽略大小写，等于0不忽略，默认不忽略，$9~/NAC/其中~代表在第九列的行内搜索（比grep的整行匹配更精确），NAC为一个基因家族名词，是搜索的内容
分析数据养成良好习惯
 运行的命令，参数等及时记录保存
 保存到sh文件，可以sh 批量运行       可以将命令可以通过vim work.sh保存为一个.sh文件，work只是3随意的命名，然后通过sh去运行，比如sh work.sh。也可以数bash
 标准输出到文件 ： 新建 > 追加>>
    >如果文件已存在，则会覆盖

任务：
添加circos可执行文件到环境变量当中：
~/.profile不同系统可能不一样
source ~/.profile

echo $PATH  显示PATH变量中的目录
which salmon 查看salmon所在目录
如果一个文件不在PATH中，系统就找不到，就会报错，解决方法，你可以将路径添加到目录，也可以直接给出指定绝对路径

Linux Shell 编程基础 简化自己的工作批量运行命令 ：omicsclass.com/article/1006

linux生物信息软件安装管理工具conda使用：omicsclass.com/article/1159
source ~/annaconda3/bin/activate
如果conda总是显示root目录下的，则将上述内容添加到.bashrc中

下面的报错是VPN问题
Collecting package metadata (repodata.json): | ERROR conda.auxlib.logz:stringify(171): Expecting value: line 1 column 1 (char 0)
Traceback (most recent call last):
  File "/home/hekun/miniconda3/lib/python3.11/site-packages/requests/models.py", line 971, in json
    return complexjson.loads(self.text, **kwargs)
```
# 软件安装
```
#转录组比对和定量 {#}
mkdir -p ~/transcriptome/soft
cd ~/transcriptome/soft

#把soft目录加大环境变量中，新安装的软件都软链到soft目录
cat <<END >>~/.bash_profile
export PATH=~/transcriptome/soft:~/anaconda3/bin:\$PATH
END

wget -c https://repo.anaconda.com/archive/Anaconda3-2023.09-0-Linux-x86_64.sh -O Anaconda3-2023.09-0-Linux-x86_64.sh
bash Anaconda3-2023.09-0-Linux-x86_64.sh -b -f -p ${HOME}/annaconda3

#必须执行
source ~/.bash_profile


conda config --add channels conda-forge # Lowest priority
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels r # Optional
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
#Anocanda清华镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
#清华通道, 最高优先级
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
conda config --set show_channel_urls yes
source ~/.bash_profile



#注意： conda安装的samtools不能使用samtools tview, 需要自己重新编译安装
conda install -y -q fastqc &
conda install -y -q  star &
conda install -y -q  HISAT2&
conda install -y -q  RSEM&
conda install -y -q stringtie &
conda install -y -q sra-tools &
conda install -y -q  trimmomatic &
conda install -y -q fastp  &
conda install bioconda::rseqc  &如果这个方法失败则使用下列的方法
#激活conda环境
conda activate 
#安装RsEQC软件
pip3 install RSeQC -i  http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
#查看是否有resqc软件
(base) [user]$ conda list#其中如果有了就是成功了，which resqc是搜索不到的，这个软件直接用里面的质量，比如read_distribution.py -h

#下载之后，放入环境变量即可使用

cd ~/transcriptome/soft
wget -c ftp://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/bedSort
wget -c ftp://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/bedGraphToBigWig
wget -c ftp://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/gtfToGenePred
wget -c ftp://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/genePredToBed


#安装gffcompare
mkdir -p ~/transcriptome/soft/gffcom
cd ~/transcriptome/soft/gffcom
git clone https://github.com/gpertea/gclib
git clone https://github.com/gpertea/gffcompare
cd gffcompare
make release
ln -sf `pwd`/gffcompare ~/transcriptome/soft

cd ~/transcriptome/soft/gffcom
git clone https://github.com/gpertea/gffread
cd gffread
make
ln -sf `pwd`/gffread ~/transcriptome/soft

#########逐个安装##################################################################
##SRA toolkit <https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=software>, 根据服务器操作系统类型下载对应的二进制编码包，下载解压放到环境变量即可使用。
##CentOS下地址：<https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.9.0/sratoolkit.2.9.0-centos_linux64.tar.gz>。
wget -c https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.9.0/sratoolkit.2.9.0-centos_linux64.tar.gz
tar xvzf sratoolkit.2.9.0-centos_linux64.tar.gz
ln -s `pwd`/sratoolkit.2.9.0-centos_linux64/bin/fastq-dump ~/transcriptome/soft
##若运行成功，则输出为 ~/transcriptome/soft/fastq-dump
which fastq-dump

##Fastqc软件安装
##yum install java-1.8.0-openjdk.x86_64 # 如果需要时安装java
cd ~/transcriptome/soft
wget -c http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip
unzip fastqc_v0.11.5.zip
chmod 755 FastQC/fastqc
##假设~/transcriptome/soft目录在环境变量中
ln -s `pwd`/FastQC/fastqc ~/transcriptome/soft/

##Trimmomatic安装

#cd ~/transcriptome/soft
#wget -c http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip
#unzip Trimmomatic-0.36.zip
#cd Trimmomatic-0.36
#echo "java -jar \$(dirname \$(readlink -f \$0))/trimmomatic-0.36.jar \$*" >trimmomatic.sh
#chmod 755 trimmomatic.sh
##假设~/transcriptome/soft目录在环境变量中
#ln -s `pwd`/trimmomatic.sh ~/transcriptome/soft/

##Salmon安装

#wget -c https://github.com/COMBINE-lab/salmon/archive/refs/tags/v1.10.1.tar.gz
#tar xvzf v1.10.1.tar.gz
#ln -s `pwd`/v1.10.1/bin/salmon ~/transcriptome/soft

###安装conda

#cd ~/transcriptome/soft
#wget -c -c https://repo.anaconda.com/archive/Anaconda2-5.1.0-Linux-x86_64.sh
#bash Anaconda2-5.1.0-Linux-x86_64.sh -b -f
##默认安装在~/anaconda2中
##cd ~/transcriptome/soft
##tar xvf samtools-1.6.tar
##cd samtools-1.6
##make
##ln -sf `pwd`/samtools ~/transcriptome/soft/

###采用STAR/HISAT2构建索引
##[HISAT2](http://ccb.jhu.edu/transcriptome/software/hisat2/index.shtml)安装
#cd ~/transcriptome/soft
#wget -c ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/downloads/hisat2-2.1.0-Linux_x86_64.zip
#unzip hisat2-2.1.0-Linux_x86_64.zip
#ln -s `pwd`/hisat2-2.1.0/* ~/transcriptome/soft

##STAR
#cd ~/transcriptome/soft
#wget https://github.com/alexdobin/STAR/archive/2.6.0c.zip -O STAR.2.6.0c.zip
#unzip STAR.2.6.0c.zip
#ln -s `pwd`/STAR-2.6.0c/bin/Linux_x86_64_static/* ~/transcriptome/soft

##RSeQC是一个python包，pip安装就可以
#cd ~/transcriptome/soft
#ln -s ~/anaconda2/include/lzo ~/anaconda2/include/python2.7/
#ln -s ~/anaconda2/include/lzo/* ~/anaconda2/include/python2.7/
#pip install -i https://pypi.tuna.tsinghua.edu.cn/simple RSeQC
##下面三个脚本 geneBody_coverage2.py, read_distribution.py, RPKM_saturation.py
##都是RSeQC的一个子工具
##HT-seq安装
#pip install -i https://pypi.tuna.tsinghua.edu.cn/simple htseq

##R包安装
#下面两句注释掉吧，在R中运行，改镜像的
##site="https://mirrors.tuna.tsinghua.edu.cn/CRAN"
##options(BioC_mirror="http://mirrors.ustc.edu.cn/bioc/")
###转录本拼装
##[StringTie](https://ccb.jhu.edu/transcriptome/software/stringtie/index.shtml?t=manual)转录本拼装
##软件安装
##stringtie
#wget -c http://ccb.jhu.edu/transcriptome/software/stringtie/dl/stringtie-1.3.4d.Linux_x86_64.tar.gz
#tar xvzf stringtie-1.3.4d.Linux_x86_64.tar.gz
#chmod 755 stringtie-1.3.4d.Linux_x86_64/stringtie
##假设~/transcriptome/soft在环境变量中
#ln -sf `pwd`/stringtie-1.3.4d.Linux_x86_64/stringtie ~/transcriptome/soft

##安装prepDE.py
##cd ~/transcriptome/soft
##wget -c https://ccb.jhu.edu/transcriptome/software/stringtie/dl/prepDE.py
##chmod 755 prepDE.py
##ln -s `pwd`/prepDE.py ~/transcriptome/soft

##TPM生成 RSEM安装
##cd ~/transcriptome/soft
##wget -c https://github.com/deweylab/RSEM/archive/v1.3.1.tar.gz -O RSEM.v1.3.1.zip
##tar xvzf RSEM.v1.3.1.zip
##cd RSEM-1.3.1
##make && make install
##wget -c https://raw.githubusercontent.com/miyagawa/cpanminus/master/cpanm -O ~/transcriptome/soft/cpanm
##cpanm Env

##差异剪接分析 {#alternative_splicing}
###软件安装
##rMATS
#pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pysam
##yum install gsl-devel.x86_64 lapack-devel blas-devel
#cd ~/transcriptome/soft
#wget -c https://sourceforge.net/projects/rnaseq-mats/files/MATS/rMATS.4.0.2.tgz
#tar xvzf rMATS.4.0.2.tgz
#python -c "import sys; print sys.maxunicode"
##输出为1114111，使用rMATS-turbo-Linux-UCS4
#cd rMATS.4.0.2/rMATS-turbo-Linux-UCS4
#chmod 755 rmats.py
##默认使用全路径调用，如果想简化些，需要修改rmats.py源文件
##第246行修改如下：
##root_dir = os.path.dirname(os.path.realpath(__file__))
#ln -s `pwd`/rmats.py ~/transcriptome/soft

##sashimiplot绘制
#pip install -i https://pypi.tuna.tsinghua.edu.cn/simple rmats2sashimiplot

# 数据下载并构建索引
####################################################
#准备一些路径变量，方便后续调用
####################################################

workdir=/u3/hekun/rnaseq  #设置工作路径
refdir=$workdir/ref
datadir=$workdir/data
scriptdir=$workdir/scripts
###################################################################
#下载参考基因组数据,并对基因组构建HISAT index
###################################################################
cd $workdir/  ###回到工作目录
cd $refdir  #进入参考基因组ref目录

#hisat2 提供常见物种基因组索引文件：
#下载参考基因组数据到ref文件夹
wget https://ftp.ebi.ac.uk/ensemblgenomes/pub/release-58/plants/gtf/triticum_aestivum/Triticum_aestivum.IWGSC.58.gtf.gz
wget https://ftp.ebi.ac.uk/ensemblgenomes/pub/release-58/plants/gff3/triticum_aestivum/Triticum_aestivum.IWGSC.58.gff3.gz
wget https://ftp.ebi.ac.uk/ensemblgenomes/pub/release-58/plants/fasta/triticum_aestivum/cdna/Triticum_aestivum.IWGSC.cdna.all.fa
wget https://ftp.ebi.ac.uk/ensemblgenomes/pub/release-58/plants/fasta/triticum_aestivum/dna/Triticum_aestivum.IWGSC.dna.toplevel.fa.gz

#gff3文件修改，因为ensemble上下载的注释上会有gene：transcript:，后续作分析带着很麻烦，所以提前处理（先提前查看文件看看有没有）
gunzip *.gz
sed 's#gene:##' Taestivum.58.gff3|sed 's#transcript:##'|less -SN
sed 's#gene:##' Taestivum.58.gff3|sed 's#transcript:##' >Taestivum.58.gff3.1 #取个名字
mv Taestivum.58.gff3.1 Taestivum.58.gff3 #重命名，覆盖原文件

#wget -c ftp://ftp.ensembl.org/pub/release-99/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.chromosome.22.fa.gz
#wget -c ftp://ftp.ensembl.org/pub/release-99/gff3/homo_sapiens/Homo_sapiens.GRCh38.99.chromosome.22.gff3.gz
#gunzip *gz

#建立索引 常见物种索引下载： http://daehwankimlab.github.io/hisat2/download/

#hisat2 建立索引非常耗内存，如果建立索引失败 被 killed

sh $scriptdir/index.sh Homo_sapiens.GRCh38.dna.chromosome.22.fa Homo_sapiens.GRCh38.99.chromosome.22.gff3

#设置参考基因组相关文件变量，方便后续使用

REF_INDEX=$refdir/Taestivum.dna.toplevel   #hisat2 索引，没有.fa
GFF=$refdir/Taestivum.58.gff3
GTF=$refdir/Taestivum.58.gtf   #这个gtf文件是由gff3文件通过脚本index.sh生成的，不是下载的。
GENE_BED=$refdir/gene.bed
GENE_LENGTH=$refdir/gene_length.txt

```
# 质控

## 一：fastqc
```
#对原始数据进行fastqc质控
#fastqc质控报告查看介绍：https://www.omicsclass.com/article/1231
cd $workdir  #回到工作目录
mkdir 1.fastqc
fastqc $datadir/*.gz  -o $workdir/1.fastqc
echo "fastqc $datadir/*.gz  -o $workdir/1.fastqc" #用于查看命令的全称

#对所有的.gz文件进行质控，并将结果输出到指定的目录，-o 是指一个参数，用于指定FastQC生成的报告文件的储存路径。这样，你就可以在目录下查看fastqc生成的报告文件，它们的后缀是.html或.zip。你可以用浏览器打开.html文件，查看每个样本的质量评估结果。
```
## 二：批量评估multiqc
```
#对fastqc结果整合与汇总
multiqc  $workdir/1.fastqc -o $workdir/1.fastqc/multiqc
echo "multiqc  $workdir/1.fastqc -o $workdir/1.fastqc/multiqc" #用于查看命令的全称
multiqc 是运行MultiQC的命令
-d 是指定要分析的目录，后面跟着目录的路径，这里是表示当前目录
-o 是指定输出报告的目录，后面跟着目录的路径，这里是 multiqc 表示在当前目录下创建一个名为multiqc的文件夹
这段代码的作用是在当前目录下搜索所有支持的生物信息学工具的输出文件，并将分析结果输出到multiqc文件夹中

查看结果

推荐：使用MobaXterm软件登陆服务器
```
## 三：使用fastp去除低质量的reads和adaptor

```
cd $workdir #回到工作目录

mkdir 2.data_qc

cd  2.data_qc

#利用fastp工具去除adapter

#--detect_adapter_for_pe  默认对双端数据则默认不使用自动检测adapter(SE可自动检测)，设置该参数，表示对双端数据也启用自动检测方法；接头序列未知  可设置软件自动识别常见接头

#--detect_adapter_for_pe    # 开启双端的接头检测(应该不同于overlap方法)

#--adapter_fasta    # 指定包含接头序列的fasta文件

# 接头序列至少6bp长度，否则将被跳过

# 可以指定任何想去除的序列，比如polyA

#对于每一个样本，执行以下操作  文件名如下格式 normal rep3_r2. fastq. gz ，tumor repl_rl. fastq. gz，tumor repl r2. fastq. gz

#使用for关键字开始一个循环，i是一个变量，用于存储每次循环中的当前文件名

#in后面跟着一个通配符表达式，表示要遍历的文件集合

#这里的通配符*表示任意长度的任意字符，_1.clean.fq.gz表示以这个字符串结尾

#所以，这个表达式匹配了data目录下的所有以_1.clean.fq.gz结尾的文件

#例如，ANTF1_FRAS202191140-1r_1.clean.fq.gz，ANTF2_FRAS202191140-1r_1.clean.fq.gz等

#分号表示一条命令的结束

#for i in /u3/hekun/rnaseq/data/*_1.clean.fq.gz;

#do # do表示循环体的开始，每次循环都会执行循环体中的命令

#使用反引号将basename命令包围，表示执行这个命令并将结果赋值给samp变量

#basename命令用于获取文件的基本名称，即去掉目录和后缀的部分

#basename命令接受两个参数，第一个是文件的完整路径，第二个是要去掉的后缀

#这里，第一个参数是i变量，表示当前循环的文件名，第二个参数是_1.clean.fq.gz，表示要去掉的后缀

#例如，如果i的值是/u3/hekun/rnaseq/data/ANTF1_FRAS202191140-1r_1.clean.fq.gz，那么basename命令的结果就是ANTF1_FRAS202191140-1r

#samp=`basename ${i} _1.clean.fq.gz`

#使用echo命令打印出一条信息，表示正在处理哪个样本

#使用双引号将字符串包围，表示字符串中的变量会被替换为实际的值

#使用美元符号和花括号将变量名包围，表示引用变量的值

#例如，如果samp的值是ANTF1_FRAS202191140-1r，那么echo命令会打印出Processing sample ANTF1_FRAS202191140-1r
#echo "Processing sample ${samp}"
#fastp --thread 1 --qualified_quality_phred 10 \
#--unqualified_percent_limit 50 \
#--n_base_limit 10 \
#-i $datadir/${samp}_1.clean.fq.gz \
#-I $datadir/${samp}_2.clean.fq.gz \
#-o ${samp}_1.clean.fastp.fq.gz \
#-O ${samp}_2.clean.fastp.fq.gz \
#--adapter_fasta $workdir/data/illumina_multiplex.fa \
#--detect_adapter_for_pe
#-h ${samp}.html -j ${samp}.json
#done


for i in /u3/hekun/rnaseq/data/*_1.clean.fq.gz;
do 
samp=`basename ${i} _1.clean.fq.gz`

echo "Processing sample ${samp}"
 
fastp --thread 1 --qualified_quality_phred 10 \
--unqualified_percent_limit 50 \
--n_base_limit 10 \
-i $datadir/${samp}_1.clean.fq.gz \
-I $datadir/${samp}_2.clean.fq.gz \
-o ${samp}_1.clean.fastp.fq.gz \
-O ${samp}_2.clean.fastp.fq.gz \
--detect_adapter_for_pe \
-h ${samp}.html \
-j ${samp}.json
done


#质控数据统计汇总：
python $scriptdir/qc_stat.py -d $workdir/2.data_qc/ -o $workdir/2.data_qc/ -p all_sample_qc
```
## 四：使用trim-galore去除低质量的reads和adaptor（与第三步骤选一个即可）
```
使用trim-galore去除低质量的reads和adaptor
创建脚本：trim_galorez_多样本qc
#!/bin/bash
for fn in /u3/2023.test/rawdata/*_1.fq.gz; # 这是一个for循环，用于遍历rawdata目录下的所有以_1.fq.gz结尾的文件，例如N10_1.fq.gz
do #循环开始
samp=`basename ${fn} _1.fq.gz` #这是一个变量赋值，用于获取文件的基本名称，即去掉_1.fq.gz的部分，例如N10
echo "Processing sample ${samp}" #这是一个输出语句，用于打印正在处理的样本名称
trim_galore -q 20 --phred33 --stringency 4 --length 25 -e 0.1 --clip_R1 9 --clip_R2 9 --fastqc --paired /u3/2023.test/rawdata/${samp}_1.fq.gz /u3/2023.test/rawdata/${samp}_2.fq.gz --gzip -o /home/hekun/cleandata/trim_galoredata
done
```
运行脚本bash trim-galore去除低质量的reads和adaptor
![image](https://github.com/826hekun/my-rnaseq/assets/157109892/229fcea3-49dd-4cae-b3e2-c76971592459)
![image](https://github.com/826hekun/my-rnaseq/assets/157109892/47c9bbd4-d96b-4782-85c3-4f78043ab951)



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

## Replot

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
