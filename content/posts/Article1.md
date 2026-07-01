+++
date = '2026-06-30T11:02:49+08:00'
draft = false



 title = 'Article1'

+++

### my first blog!记录搭建全部过程！

###当你看到这条消息的时候，恭喜你！终于成功了！！！

###前言

我想在我第一篇blog里面记录一下我用hugo搭建blog并将其放进GitHub的全部过程和经历（包括遇到的各种问题和解决方案）。我认为这是一个很难忘的经历值得去记录！

但是我并不是很懂这方面的内容，很多话术都不是专业的QAQ，只不过是自己的复盘~~~

### part1：用hugo搭建个人blog~

1.下载Hugo：我是根据教程的指引到GitHub上面下载的最新版本：v0.163.3

遇到的问题：

​      1.一开始打不开GitHub，按照指引去到了镜像地址下载！但是这是这个应该是错误的，正确的里面在版本下还有各种不同的压缩包可选择！

​      2.一定要下载extended版！后面的theme需要这个版本的！

2.创建放博客的文件夹：按照教程我在D盘中创建了一个project文件夹，又在其中设了一个 Obsidian-Hugo，并且进入文件夹后再创建一个名为 bin 的文件夹，我们专门放安装的脚本。再把上面下载的内容解压到这个 bin 文件夹中。

3.配置环境变量：把这个 hugo 程序配置到环境变量去，这样我们才能在其他位置也使用 hugo. exe 提供的命令。在环境变量中系统变量的path中添加我刚下载hugo的位置！

查看是否生效：hugo version，看到输出版本号就是生效了。

4.创建博客网站：在CMD中首先cd到我们放hugo的目录，执行 `hugo new site 博客名` ，就可以创建博客了。我设的博客名是myBlog：）然后就能看到在文件夹Obsidian-Hugo中有一个叫myBlog的文件夹并且里面有很多东西！

5.创建文章：创建好了站点后，现在网站中还什么内容都没有，我们可以创建一篇文章来进行一下测试。现在我们进入站点目录，并且创建文章。在CMD中（在刚刚目录的基础上进入myBlog下输入）hugo new posts/Articles 1. md执行后可以看到提示已经创建了一篇名为 Articles 1 的文章与其所属路径。在content-posts里面！这时候可以打开这个Articles 1.md（需要下载一个可以打开这个Markdown文件的软件！我找了半天还是跟这个教程下载了一个Typora，下载很方便很容易！我是在网上找的教程指引下载的~）

在这里我们需要把 draft（草稿） = true 修改为 draft = false 来表示这并不是一篇草稿。草稿的话，到时候启动博客的时候，你会看不到这个内容。然后保存关闭！

6.设置主题！Hugo 你要是不设置主题，你看不到内容。可以到官网theme里面挑选喜欢的主题

这个也是我非常头疼的一个环节！！！后面不成功全是因为这个环节出现问题了！！！很讨厌啦！

教程内容：点击进入页面后，可以看到 download 进行下载。（到GitHub界面点击code下面有个download zip，下载后把他放到theme文件夹中，进入 hugo 的配置文件（hugo.toml，把 theme = ‘<theme中文件名！>’ 这行代码加进去保存即可。

但是后面在测试的时候出现了很多问题！

7.本地访问测试！在刚刚CMD目录下面输入hugo server，他会出现一个网址在最下面！按住control 点击这个网址就是你的blog了！

想得美！一开始这个是什么都没显示！

遇到的情况和问题：

情景1：

点进去后下面直接是WARN 2026/06/29 17:34:49 found no layout file for "HTML" for kind "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.在网上看到也老外有类似的经历！下面好心人给的答案是

1. Does not specify the theme in the config file

2. Does not have any content

   我呢经历了一系列操作！把hugo删了改成最新版本！把一开始的theme删了！换了一个theme，然后之前是把theme下载解压后复制到里面，现在严格按照教程直接在theme中解压

反正呢，也不知道是哪一步起效果了：（总之不报这个错误了！页面能进去了。。。但是找不到页面了。。。报错增至4项：）###也是这个时候我终于想起来。。。我可以去问ai....【挠头】

事实证明，ai真的超好用！尤其对我这样的小白！【好感度+10086】

情景2：

WARN  found no layout file for "html" for kind "taxonomy": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "html" for kind "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "html" for kind "page": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "html" for kind "section": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.

ai说【超严肃】：这是 Hugo **典型的"主题/布局文件未生效"问题**——Hugo 在 `layouts/`目录和主题目录下都找不到任何 HTML 模板（home、page、section、taxonomy 全都没有），所以渲染不出页面，浏览器显示 404/No Found。![78287674046](C:\Users\99418\AppData\Local\Temp\1782876740467.png)

按照ai给的指示进行查找：

dir
dir themes
type config.toml

终于发现问题在于：你在 `C:\Users\99418>`这个目录下执行了命令，这里确实有一个 `themes`文件夹，并且里面有一个叫 `anank`的文件夹。

这个应该是我第一个下的theme，就是因为没有直接在theme下面解压！路径不对！它找不到了，而且我后面还没删干净【挠头】

接下来在hugo目录下找：

dir

dir themes

发现现在的目录结构非常标准，而且在 `themes`文件夹下确实有一个名为 `stack`的主题。这说明主题已经成功放在了正确的项目目录中。之前看到的报错有很大可能是因为 Hugo 还没有读取到这个 `stack`主题。需要告诉 Hugo 启用它。

咱也不知道QAQ为什么一开始没写进去QAQ

后面发现。。。hugo没下扩展版的，不适用这个theme，连夜重下了一个hugo

总之！经过了这些问题之后终于是好了！

要结束了吗？NO！![78287736149](C:\Users\99418\AppData\Local\Temp\1782877361495.png)

看到了没，没有我写的内容QAQ，找了半天原因（真的是半天！）

最后发现不是我错了，这是设计师的小巧思：|【没招了】原来后面加上/posts/就可以了！Stack 主题的首页（Homepage）默认不是“文章列表页”，而是一个“个人主页/档案页（Profile Page）”。【我投降】

至此第一个篇章完成{完结撒花！！！}

