# shell字符串处理
## 字符串操作（长度，读取，替换）
表达式      |含义
-----------|-------------
${#string} | $string的长度
${string:position}|在$string中，从位置$position开始提取子串
${string:position:length}|在$string中，从位置$position开始提取长度为$length的子串
${string#substring}|从变量$string的开头删除最短匹配$substring的子串
${string##substring}|从变量$string的开头，删除最长匹配$substring的子串
${string%substring}|从变量$string的结尾，删除最短匹配$substring的子串
${string%%substring}|从变量$string的结尾，删除最长匹配$substring的子串
${string/substring/replacement}|使用$replacement，来代替第一个匹配的$substring
${string//substring/replacement}|使用$replacement, 代替所有匹配的$substring
${string/#substring/replacement}|如果$string的前缀匹配$substring, 那么就用$replacement来代替匹配到的$substring
${string/%substring/replacement}|如果$string的后缀匹配$substring, 那么就用$replacement来代替匹配到的$substring
###字符串操作举例：
>1 长度

>~~~
>$ string=linuxeye 
>$ echo {#string} 
>8
>~~~
>2 截取字串

>~~~
>$ string=linuxeye
>$ echo ${string:5} 
>eye 
>$ echo ${string:0:5} #默认从0开始，可省略，如下 
>linux 
>$ echo ${string::5} 
>linux
>~~~
>3 字符串删除 

>~~~
>$ redis_file=c:/windows/src/redis-2.8.4.tar.gz 
>$ echo ${redis_file#/} 
>c:/windows/src/redis-2.8.4.tar.gz 
>$ echo ${redis_file#*/} 
>windows/src/redis-2.8.4.tar.gz 
>$ echo ${redis_file##*/} 
>redis-2.8.4.tar.gz 
>echo ${redis_file%/*} 
>c:/windows/src 
>$ echo ${redis_file%%/*} 
>c:
>~~~
> ${变量名#substring正则表达式}从字符串开头开始配备substring,删除匹配上的表达式。

> ${变量名%substring正则表达式}从字符串结尾开始配备substring,删除匹配上的表达式。 

>注意：${redis_file##*/},${redis_file%/*} 分别是得到文件名，或者目录地址最简单方法。

>4 字符串替换

>~~~
>$ echo ${redis_file/\//\\} 
>c:\windows/src/redis-2.8.4.tar.gz 
>$ echo ${redis_file//\//\\} 
>c:\windows\src\redis-2.8.4.tar.gz 
>${变量/查找/替换值} 一个"/"表示替换第一个，"//"表示替换所有,
当查找中出现了："/"请加转义符"\/"表示。
>~~~

##判断读取字符串值
表达式      |含义
-----------|-------------
${var} | 变量var的值, 与$var相同
${var-DEFAULT}|如果var没有被声明, 那么就以$DEFAULT作为其值
${var:-DEFAULT}|如果var没有被声明, 或者其值为空, 那么就以$DEFAULT作为其值，判断var变量是否没有定义
${var=DEFAULT}|如果var没有被声明, 那么就以$DEFAULT作为其值
${var:=DEFAULT}|如果var没有被声明, 或者其值为空, 那么就以$DEFAULT作为其值 ，判断var变量是否没有定义，并确保变量始终有值
${var+OTHER}|如果var声明了, 那么其值就是$OTHER, 否则就为null字符串
${var:+OTHER}|如果var被设置了, 那么其值就是$OTHER, 否则就为null字符串
${var?ERR_MSG}|如果var没被声明, 那么就打印$ERR_MSG
${var:?ERR_MSG}|如果var没被设置, 那么就打印$ERR_MSG
${!varprefix*}|匹配之前所有以varprefix开头进行声明的变量
${!varprefix@}|匹配之前所有以varprefix开头进行声明的变量

###判断读取字符串值举例：
>~~~
>$ output=${FILE:-UNSET} 
>$ echo $output 
>UNSET 
>$ FILE=/root/lnmp 
>$ output=${FILE:-UNSET} 
>$ echo $output 
>/root/lnmp 
>~~~
>对变量的路径进行操作时，最好先判断路径是否为非空,如下path变量没有定义，则取/tmp，防止变量没定义误删除： 

>$ find ${path-/tmp} -name *.tar.gz -type f | xargs rm -f