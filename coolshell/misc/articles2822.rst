.. _articles2822:

使用grep恢复被删文件内容
========================

2010年8月24日 `陈皓 <http://coolshell.cn/articles/author/haoel>`__

在Unix/Linux下，最危险的命令恐怕就属rm命令了，每次在root下使用这个命令的时候，我都要盯着命令行看上几分钟才敢把回车敲下去。以前，看到同事在脚本中使用rm命令
—— ``rm {$App_Dir}/*``
。因为脚本没有判断变量$App\_Dir是否为空，结果，在一次用root操作的时候，整个操作系统一下就不见了，还好只是开发机。从此，我们大家都再也不敢使用rm命令了。

这里给大家介绍一个小技巧用来恢复一些被rm了的文件中的数据。我们知道，rm命令其实并不是真正的从物理上删除文件内容，只过不把文件的inode回收了，其实文件内容还在硬盘上。所以，如果你不小删除了什么比较重要的程序配置文件的时候，我们完全可以用grep命令在恢复，下面是一个恢复示例：

::

    grep -a -B 50 -A 60 'some string in the file' /dev/sda1 > results.txt

说明：

-  关于grep的-a意为–binary-files=text，也就是把二进制文件当作文本文件。
-  -B和-A的选项就是这段字符串之前几行和之后几行。
-  /dev/sda1，就是硬盘设备，
-  > results.txt，就是把结果重定向到results.txt文件中。

如果你幸运的话，你就可以看到被恢复的内容了。这正是Unix的简单哲学（详见《\ `Unix传奇下篇 <http://coolshell.cn/articles/2324.html>`__\ 》）——\ **所有的设备都是文件**\ 。

当然，我还是建议你把root用户的rm的命令用alias换成别一个脚本，那个脚本会帮你把删除的文件放到某个地方。

.. |image6| image:: /coolshell/static/20140922094136638000.jpg

.. note::
    原文地址: http://coolshell.cn/articles/2822.html 
    作者: 陈皓 

    编辑: 木书架 http://www.me115.com