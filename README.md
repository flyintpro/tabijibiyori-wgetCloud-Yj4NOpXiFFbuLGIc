
转载请注明出处：


　　在Linux系统中，软连接（Symbolic Link）是一种特殊类型的文件链接，类似于Windows系统中的快捷方式。它允许用户通过一个文件路径访问另一个文件或目录，而不需要拥有原始文件或目录的实际拷贝。软连接是通过文件名来引用文件或目录，而不是通过它们的物理位置来引用。


### 一、相关语法


　　软连接命令的基本语法如下：




```
ln -s [源文件或目录] [软连接文件名]
```


　　其中，`-s`选项表示创建软连接。如果不加`-s`选项，则会创建硬链接。


### 二、创建软连接：


* 示例命令：`ln -s /usr/local/bin/python3 /usr/bin/python`
* 说明：此命令创建了一个名为`python`的软连接文件，指向了`/usr/local/bin/python3`这个源文件。创建软连接时，会在指定的目录下创建一个软连接名称。



  root@controller1:/usr/bin\# ln \-s /usr/local/bin/python2\.7 /usr/bin/python4  root@controller1:/usr/bin\#



```
##再次执行则提示异常root@controller1:/usr/bin# ln -s /usr/bin/python2.7 /usr/bin/python4
ln: failed to create symbolic link '/usr/bin/python4': File exists
root@controller1:/usr/bin#
root@controller1:/usr/bin# ln -s /usr/bin/python2.7 /usr/bin/python5
root@controller1:/usr/bin#
```


　　正确的软连接创建是绿色显示，错误的是红色显示，


![](https://img2024.cnblogs.com/blog/1110857/202412/1110857-20241201124424714-817356119.png)


### 三、查看软连接：


* `ls -l /usr/bin/python`
* 说明：此命令将显示软连接文件`python`的详细信息，其中包含软连接的源文件路径（`/usr/local/bin/python3`），并以箭头符号（`->`）与软连接名称分开。




```
root@controller1:/usr/bin# ls -l /usr/bin/python5
lrwxrwxrwx 1 root root 18 Dec  1 12:39 /usr/bin/python5 -> /usr/bin/python2.7
root@controller1:/usr/bin#
```


* `l` 表示这是一个软连接（Symbolic Link）。
* `rwxrwxrwx` 是软连接的权限（尽管这些权限通常不影响软连接本身的行为，而是影响对软连接指向的目标的访问）。
* 1 是链接数（对于软连接来说，这个值通常不重要）。
* `user` 是软连接的所有者。
* `user` 是软连接所属的用户组。
* `9` 是软连接文件本身的大小（以字节为单位），这通常是一个很小的值，因为软连接只是包含了一个指向目标的路径。
* `date` 和 `time` 是软连接的最后修改日期和时间。
* `linkname` 是软连接的名称。
* `-> targetpath` 是软连接指向的目标文件或目录的路径。


### 四、删除软连接：


* `rm /usr/bin/python`
* 说明：此命令将删除软连接文件`python`，但不会影响源文件`/usr/local/bin/python3`的存在。


 


 本博客参考[milou加速器](https://jiechuangmoxing.com)。转载请注明出处！
