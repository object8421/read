.. _articles1724:

恐怖的C++语言
=============

2009年11月11日 `陈皓 <http://coolshell.cn/articles/author/haoel>`__

|我爱C++|
Linus曾经(2007年9月)在新闻组\ `gmane.comp.version-control.git <http://news.gmane.org/gmane.comp.version-control.git>`__\ 里和一个微软的工程师（Dmitry
Kakurin）争执过用C还是用C++，当时的那个微软的工程师主要是在做Git的Windows版，但他却发现Git的源码居然是C语言写的，而不是C++，于是他（Dmitry
Kakurin）在Linux社区里发贴表示对Linux的不满，语言很直接：

    Pure C as opposed to C++. No idea why. Please don’t talk about
    portability, it’s BS.
    （纯C写的，而不是C++，不知道为什么，请别告诉我是为了移植性，这完全是胡扯。）

Linux之父Linus
Torvalds马上跟贴，在贴子中，Linus言辞很直接，直接表明C++是一个很恐怖的语言，他在\ `**贴子** <http://thread.gmane.org/gmane.comp.version-control.git/57643/focus=57918>`__\ 中说：

    **\*YOU\*** are full of bullshit. C++ is a horrible language. It’s
    made more horrible by the fact that a lot of substandard programmers
    use it.
    （你才是完全在胡扯。C++是一门很恐怖的语言，而比它更恐怖的是很多不合格的程序员在使用着它）

Linus的这个观点我是比较同意的，我个人也在几年前的《\ `STL
String类的写时才拷贝 <http://blog.csdn.net/haoel/archive/2004/06/23/24058.aspx>`__\ 》以及以后的一些文章中表达过C++的确并不是一个很成熟的语言，这种观点一直都围绕着我。这是因为它的学习成本实在是太高了，编译器和类背着你做了很多你不知道的事，而且，C++非常容易地出错和发生很多意想不到的问题。

当然，这篇文章并不是要继续声讨C++，也不是回顾以前的某个事件。我们这里只谈技术。昨天，我在网上看到一个邪恶的C++的示例，在这里给大家share一下，让大家看看C++这种编程语言的恐怖和邪恶的一面。下面的这个例子，比那个“#define
 private  public”还更加邪恶。

请看下面这段代码，你能告诉我它会输出什么吗？（注意main函数中高亮的那一行）

::

    #include 
    #include 

    typedef int UINT4;
    using namespace std;
    class Hack
    {
    };

    Hack& operator< (Hack &a , Hack &b)
    {
        std::cerr << "小于操作符\n";
        return a;
    }

    Hack& operator> (Hack &a, Hack &b)
    {
        std::cerr <<  "大于操作符\n";
        return a;
    }

    int main(int argc, char ** argv)
    {
        Hack vector;
        Hack UINT4;
        Hack foo;

        vector foo;

    return(0);
    }

|不是吧|\ 是的，上面这段代码如果只看main函数中的那句“vector
foo”，你会觉得很眼熟，然而，事情并非那么简单，我们可以看到vector,
UINT4和foo都是Hack类的实例，这就是邪恶的开始，那两个尖括号<
>则成了两个运算符，大于和小于，这两个运算符却又被重载了。其实，真正的语句是：

::

    vector.operator<(UNIT4).operator>(foo);

所以，所有的一切都符合我们的C++的规范和语法，自然程序也能被顺利编译通过（至少，在我的G++上是没有问题的）。而整个程序的运行结果自然是：

::

    $ ./horror
    小于操作符
    大于操作符

是的，如果你通晓C++的一切的一切，你自然不会对这段程序感到惊奇。这样的事情在C/C++的世界中并不少见，要搞乱C/C++的代码并不是一件难事，花样多得数不胜数，只要看看《\ `6个变态的C语言Hello
World程序 <http://coolshell.cn/articles/914.html>`__\ 》你就知道了，而且，还有一个简单的教程《\ `如何加密/混乱C源代码 <http://coolshell.cn/articles/933.html>`__\ 》告诉你一些简单的做法。

那么，如果你有一天在读程序中看到“vector foo”，你会觉得那只是一个幻觉吗？

（全文完）

.. |我爱C++| image:: /coolshell/static/20140922114656164000.jpg
   :target: http://coolshell.cn//wp-content/uploads/2009/11/cpp.jpg
.. |不是吧| image:: /coolshell/static/20140922114656285000.jpg
.. |image8| image:: /coolshell/static/20140922114656363000.jpg

.. note::
    原文地址: http://coolshell.cn/articles/1724.html 
    作者: 陈皓 

    编辑: 木书架 http://www.me115.com