Python 2/3 同时使用:
不论python2还是python3，python可执行文件都叫python.exe，在cmd下输入python得到的版本号取决于环境变量里哪个版本的python路径更靠前，毕竟windows是按照顺序查找的。

当python脚本需要python2运行时，只需在脚本前加上:<br>
#! python2<br>
当python脚本需要python3运行时，只需在脚本前加上:<br>
#! python3<br>

当需要python2的pip时:<br>
py -2 -m pip install xx<br>
当需要python3的pip时:<br>
py -3 -m pip install xx<br>
