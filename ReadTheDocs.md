# 文档如何同步到ReadTheDocs

我这几天尝试着在手机上利用github, sphinx, eeadthedocs发布我的markdown格式读书笔记，终于成功。

## 第一步

在github上新建一个项目，在手机上clone下来。

## 第二步

在termux里面安装sphinx、主题以及markdown插件：

```
pip install sphinx sphinx_rtd_theme recommonmark
```
别的主题可以在 [sphinx theme](https://sphinx-themes.org/)中找到。

## 第三步

运行 sphinx-quickstart，做适当设置。项目名称可以设置为中文的，语言设置为 zh_CN。

## 第四步

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

   contents
   202*


目录与索引
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

```
几个标题地方都可以写自己的东西。glob指令和底下的文件通配符之间要隔一个空行。我所有的文件都是用日期作为文件名，所以用202*作为文件名通配符。用glob指令和通配符，就不需要每次新建文件之后打开编辑index.rst和contents.rst了。

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
   

目录与索引
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
```
内容可以自己定，当然得跟目录有关。不过不能引用contents自身。

## 第六步

用github注册readthedocs.io。导入刚才push的项目。语言选择简体中文，编程语言根据实际情况来选择，我这是笔记，选择Only Words。

高级设置里面，Disable Analytics勾选，毕竟没有Google 分Analytics Tracking ID。

## 第七步

进入termux，进入文档主目录，make html。完成后git push。等待readthedocs自动构建，稍等片刻，就可以打开网址阅读文档。

## 结语

以后每次编辑完文档就make html一次，然后 git push，readthedocs这边就会自动构建。
