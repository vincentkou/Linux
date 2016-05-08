# shell字符截断

## 如果是文件路径的进行字符截断可以用basename和dirname这两个工具
basename可以从一个文件路径中截一个文件名

``` sh
$ basename /root/lnmp/lnmp_install.sh 
> lnmp_install.sh
```
dirname可以从一个文件路径中截到一个目录路径

``` sh
$ dirname /root/lnmp/lnmp_install.sh
> /root/lnmp
```
## 不使用外部工具进行字符截断
bash有自带的功能来对变量进行字符截断，一般使用”#”， “##”， “%%”， “%”， “*” 组合来实现。

``` sh
$ teststring=www.linuxeye.com
$ echo ${teststring#*.} 
linuxeye.com 
$echo ${teststring##*.} 
com
$ echo ${teststring%.*} 
www.linuxeye 
$ echo ${teststring%%.*} 
www
```
> * “#”表示从字符开始部分除去，一旦匹配则立即除去

> * “##”表示从字符开始部分除去，会搜整个字符串最长的和的匹配来除去

> * “%”表示从字符结束的部分除去，一旦匹配成公则立即除去
> * “%%”表示从字符结束的部分开始除去，会搜寻整个字符穿中最长的匹配来除去

> * “*”统配符

```sh
	$ echo ${dir##*/} 
	lnmp_install.sh 
	$ echo ${dir%/*} 
	/root/lnmp 
	$ echo ${dir##*.} 
	sh
```

## 不利用工具取文件名和目录
```sh
$ echo ${dir##*/} 
lnmp_install.sh 
$ echo ${dir%/*} 
/root/lnmp 
$ echo ${dir##*.} 
sh
```

> * 在路径中取文件名: ${path##*/} (与basename相同功能)

> * 在路径中取目录路径: ${path%/*} (与dirname相同功能)

> * 取文件的扩展名: ${path##*.}
