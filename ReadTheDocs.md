# 文档如何同步到ReadTheDocs

我这几天尝试着在手机上利用github, sphinx, readthedocs发布我的markdown格式读书笔记，终于成功。

## 第一步

在github上新建一个项目，在手机上clone下来。

## 第二步

在termux里面安装sphinx、主题以及markdown插件：

```
pip install sphinx sphinx_rtd_theme recommonmark

pip install sphinxcontrib-mermaid
```
别的主题可以在 [sphinx theme](https://sphinx-themes.org/)中找到。

**这一步不需要了。**

## 第三步

运行 sphinx-quickstart，做适当设置。项目名称可以设置为中文的，语言设置为 zh_CN。

**这一步也可以不需要。**

## 第四步

**如果不执行第三步，这一步所涉及的两个文件就需要手工创建。**

修改index.rst和conf.py。

conf.py：

```
extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.doctest',
    'sphinx.ext.intersphinx',
    'sphinx.ext.todo',
    'sphinx.ext.coverage',
    'sphinx.ext.mathjax',
    'sphinx.ext.ifconfig',
    'sphinx.ext.viewcode',
    'sphinx.ext.githubpages',
    'sphinxcontrib.mermaid',
    'recommonmark'
]
source_suffix = ['.rst', '.md']
html_theme = 'sphinx_rtd_theme'

```
index.rst：

```
欢迎查看向明的读书笔记！
===========================

.. toctree::
   :maxdepth: 1
   :caption: 目录:
   :glob:
   :reversed: 

   contents
   202*


```
几个标题地方都可以写自己的东西。glob指令和底下的文件通配符之间要隔一个空行。我所有的文件都是用日期作为文件名，所以用202*作为文件名通配符。用glob指令和通配符，就不需要每次新建文件之后打开编辑index.rst和contents.rst了。reversed指令是倒序排列。底下默认还有一些模块索引和搜索链接，因为我这是文本文档，不是代码文档，无法生成模块索引，就都不要了。

## 第五步

在resource目录下面新建一个contents.rst。
```
读书笔记目录
===========================

.. toctree::
   :maxdepth: 1
   :caption: 目录:
   :glob:

   202*

```
内容可以自己定，当然得跟目录有关。不过不能引用contents自身。

## 第六步

**前面简化掉那几步是因为readthedocs自带了相应的文件，而且自己会执行相应的操作。**

用github注册readthedocs.io。导入刚才push的项目。语言选择简体中文，编程语言根据实际情况来选择，我这是笔记，选择Only Words。

高级设置里面，Disable Analytics勾选，除非你有Google Analytics Tracking ID。

**似乎如果勾选“生成epub文件”会导致readthedocs出错，不能完成自动构建。**

## 第七步

进入termux，进入文档主目录，make html。完成后git push。等待readthedocs自动构建，稍等片刻，就可以打开网址阅读文档。

**不需要make htnl了，直接git push就行。**

## 结语

以后每次编辑完文档就make html一次，然后 git push，readthedocs这边就会自动构建。

**不需要make htnl了，直接git push就行。**
