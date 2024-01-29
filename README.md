# my-rnaseq
争取早日成为生信高手
# Linux操作基础 
orkj3401772k2ei3
0heyuanyu@

home光标回到开头
clear清屏

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

# 软件安装

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


