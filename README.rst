sphinx 文档工程
***********************

所有工程
____________________

命令如下::

    ➜  doc_sphinx find . -iname "conf.py"
    ./doc_design/source/conf.py
    ./doc_algo/source/conf.py
    ./doc_workdirection/source/conf.py
    ./doc_cs/source/conf.py
    ./doc_construct/source/conf.py
    ./doc_lang/source/conf.py


具体包含以下几个工程

* design 设计模式，软件工程
* algo 算法
* workdirection 工作方向
* cs 计算机科学
* construct 工程构建
* lang 编程语言




屏蔽以下文件夹
____________________________

命令如下::

    ➜  doc_sphinx find . -iname "conf.py"
    ./doc_design/source/conf.py
    ./doc_algo/source/conf.py
    ./doc_workdirection/source/conf.py
    ./doc_cs/source/conf.py
    ./doc_construct/source/conf.py
    ./doc_lang/source/conf.py


安装路径
___________________

执行以下安装命令::

    pip install sphinx


其他的按照vscode的提示安装即可

具体安装库，可参考以下几点::

    ➜  DocSphinx git:(main) pip list | grep sphinx
    sphinx-autobuild              2021.3.14
    sphinxcontrib-applehelp       1.0.2
    sphinxcontrib-devhelp         1.0.2
    sphinxcontrib-htmlhelp        1.0.3
    sphinxcontrib-jsmath          1.0.1
    sphinxcontrib-qthelp          1.0.3
    sphinxcontrib-serializinghtml 1.1.4


    pip install rstcheck
    pip install sphinx sphinx-autobuild



