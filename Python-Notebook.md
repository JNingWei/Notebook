
logging模块
----

#### 日志级别大小：

CRITICAL > ERROR > WARNING > INFO > DEBUG > NOTSET

#### 可自定义日志级别：


    import logging

    logging.basicConfig(
                        level=logging.WARNING,
                        format='%(asctime)s %(levelname)s %(message)s',
                        filename='myapp.log',
                        filemode='w')

    logging.debug('Debug message')
    logging.info('Info message')
    logging.warning('Warning message')


**logging.basicConfig 函数** 各参数:

> filename: 指定日志文件名
>
> filemode: 和file函数意义相同，指定日志文件的打开模式，'w'或'a'
>
> format: 指定输出的格式和内容，format可以输出很多有用信息，如上例所示:
>
> %(levelno)s: 打印日志级别的数值
>
> %(levelname)s: 打印日志级别名称
>
> %(pathname)s: 打印当前执行程序的路径，其实就是sys.argv[0]
>
> %(filename)s: 打印当前执行程序名
>
> %(funcName)s: 打印日志的当前函数
>
> %(lineno)d: 打印日志的当前行号
>
> %(asctime)s: 打印日志的时间
>
> %(thread)d: 打印线程ID
>
> %(threadName)s: 打印线程名称
>
> %(process)d: 打印进程ID
>
> %(message)s: 打印日志信息
>
> datefmt: 指定时间格式，同time.strftime()
>
> level: 设置日志级别，默认为logging.WARNING
>
> stream: 指定将日志的输出流，可以指定输出到sys.stderr,sys.stdout或者文件，默认输出到sys.stderr，
>
> 当stream和filename同时指定时，stream被忽略

[python 的日志logging模块学习](http://blog.csdn.net/yatere/article/details/6655445)

[python logging模块使用教程](http://www.jianshu.com/p/feb86c06c4f4)

[使用python的logging模块](http://kenby.iteye.com/blog/1162698)

---

---

