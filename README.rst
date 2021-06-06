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


branch
-------------------

multi repo opr::

    ➜  DocSphinx git:(main) git remote -v
    origin	git@github.com:CAUCHY2932/DocSphinx.git (fetch)
    origin	git@github.com:CAUCHY2932/DocSphinx.git (push)


    git remote add mirror https://gitee.com/aaron2932/DocSphinx.git

    ➜  DocSphinx git:(main) git remote -v
    mirror	https://gitee.com/aaron2932/DocSphinx.git (fetch)
    mirror	https://gitee.com/aaron2932/DocSphinx.git (push)
    origin	git@github.com:CAUCHY2932/DocSphinx.git (fetch)
    origin	git@github.com:CAUCHY2932/DocSphinx.git (push)

    ➜  DocSphinx git:(main) ✗ git add -u
    ➜  DocSphinx git:(main) ✗ git commit -m "feat: add gitee and github"
    [main e101d58] feat: add gitee and github
     1 file changed, 19 insertions(+)
    ➜  DocSphinx git:(main) git push mirror
    Username for 'https://gitee.com': aaron2932
    Password for 'https://aaron2932@gitee.com':
    Counting objects: 3, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 477 bytes | 477.00 KiB/s, done.
    Total 3 (delta 2), reused 0 (delta 0)
    remote: Powered by GITEE.COM [GNK-5.0]
    To https://gitee.com/aaron2932/DocSphinx.git
       c506643..e101d58  main -> main
    ➜  DocSphinx git:(main)


