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

**1.下载Hugo：**我是根据教程的指引到GitHub上面下载的最新版本：v0.163.3

遇到的问题：

​      1.一开始打不开GitHub，按照指引去到了镜像地址下载！但是这是这个应该是错误的，正确的里面在版本下还有各种不同的压缩包可选择！

​      2.一定要下载extended版！后面的theme需要这个版本的！

**2.创建放博客的文件夹：**按照教程我在D盘中创建了一个project文件夹，又在其中设了一个 Obsidian-Hugo，并且进入文件夹后再创建一个名为 bin 的文件夹，我们专门放安装的脚本。再把上面下载的内容解压到这个 bin 文件夹中。

**3.配置环境变量：**把这个 hugo 程序配置到环境变量去，这样我们才能在其他位置也使用 hugo. exe 提供的命令。在环境变量中系统变量的path中添加我刚下载hugo的位置！

查看是否生效：hugo version，看到输出版本号就是生效了。

**4.创建博客网站**：在CMD中首先cd到我们放hugo的目录，执行 `hugo new site 博客名` ，就可以创建博客了。我设的博客名是myBlog：）然后就能看到在文件夹Obsidian-Hugo中有一个叫myBlog的文件夹并且里面有很多东西！

**5.创建文章**：创建好了站点后，现在网站中还什么内容都没有，我们可以创建一篇文章来进行一下测试。现在我们进入站点目录，并且创建文章。在CMD中（在刚刚目录的基础上进入myBlog下输入）hugo new posts/Articles 1. md执行后可以看到提示已经创建了一篇名为 Articles 1 的文章与其所属路径。在content-posts里面！这时候可以打开这个Articles 1.md（需要下载一个可以打开这个Markdown文件的软件！我找了半天还是跟这个教程下载了一个Typora，下载很方便很容易！我是在网上找的教程指引下载的~）

在这里我们需要把 draft（草稿） = true 修改为 draft = false 来表示这并不是一篇草稿。草稿的话，到时候启动博客的时候，你会看不到这个内容。然后保存关闭！

**6.设置主题**！Hugo 你要是不设置主题，你看不到内容。可以到官网theme里面挑选喜欢的主题

这个也是我非常头疼的一个环节！！！后面不成功全是因为这个环节出现问题了！！！很讨厌啦！

教程内容：点击进入页面后，可以看到 download 进行下载。（到GitHub界面点击code下面有个download zip，下载后把他放到theme文件夹中，进入 hugo 的配置文件（hugo.toml，把 theme = ‘<theme中文件名！>’ 这行代码加进去保存即可。

但是后面在测试的时候出现了很多问题！

**7.本地访问测试！**在刚刚CMD目录下面输入hugo server，他会出现一个网址在最下面！按住control 点击这个网址就是你的blog了！

***想得美！一开始这个是什么都没显示！***

#### **遇到的情况和问题：**

**情景1：**

点进去后下面直接是WARN 2026/06/29 17:34:49 found no layout file for "HTML" for kind "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.在网上看到也老外有类似的经历！下面好心人给的答案是

1. Does not specify the theme in the config file

2. Does not have any content

   我呢经历了一系列操作！把hugo删了改成最新版本！把一开始的theme删了！换了一个theme，然后之前是把theme下载解压后复制到里面，现在严格按照教程直接在theme中解压

反正呢，也不知道是哪一步起效果了：（总之不报这个错误了！页面能进去了。。。但是找不到页面了。。。报错增至4项：）###也是这个时候我终于想起来。。。我可以去问ai....【挠头】

事实证明，ai真的超好用！尤其对我这样的小白！【好感度+10086】

**情景2：**

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

看到了没，里面没有我写的内容QAQ，找了半天原因（真的是半天！）

最后发现不是我错了，这是设计师的小巧思：|【没招了】原来后面加上/posts/就可以了！Stack 主题的首页（Homepage）默认不是“文章列表页”，而是一个“个人主页/档案页（Profile Page）”。【我投降】

#### **至此第一个篇章完成{完结撒花！！！}**

### part2：严格按照老师给的资料安装Git

在网上找到Git的官网然后下载下来

接着一路next

不放心又去找了相关教程

总之这块没难度！

### part3：将博客托管到Github

这边相关教程就少很多了，我就让ai辅助我（其实是我辅助ai）按照老师给的指导，让他帮我做

但是后面我就有点被动！也不知道在干什么！不如上面，至少当时我还知道我在干嘛

##### 核心思路：用 Hugo 把你的博客生成纯 HTML 文件 -> 把 HTML 文件放到 GitHub 上 -> 用 GitHub 提供的免费域名访问。

**1.生成静态文件：**在CMD中进入我的博客目录：输入hugo -D

执行后，你的博客目录下会多出一个名为 `public`的文件夹，这里面就是最终要上传到网上的纯 HTML 网页文件

**2.初始化Git仓库并进入目录：**

- 继续在命令行输入 `cd public`进入这个文件夹。
- 输入 `git init`，这会在 `public`文件夹里生成一个隐藏的 `.git`文件夹，把它变成一个 Git 仓库

**3.使用 GitHub Desktop 上传：**

下载Github Desktop软件（登录Github账号，这个过程很漫长，老是登不进去，要耐心等3min，关联账号！）

在软件左上角点击 `File`-> `Add Local Repository...`。

选择你刚才的 `public`文件夹，点击 `Open`。

在弹出的窗口中，点击 `Create repository`。

在软件下方的 `Summary`框里随便写点什么（比如 "First commit"），然后点击 **Commit to main**。

接着点击右上角的 **Publish repository**（或者 `Push origin`），把它推送到 GitHub 上。

**4.在 GitHub 上创建仓库（关键点）**

- 打开浏览器，登录 GitHub。
- 点击右上角的 `+`号 -> `New repository`。
- **仓库名（Repository name）** 必须严格填写：`你的GitHub用户名.github.io`（注意全部小写，比如你的用户名是 `zhangsan`，那就填 `zhangsan.github.io`）。
- 选择 `Public`，不要勾选 `Initialize this repository with a README`，然后点击 `Create repository`。

**5.访问你的博客：**

- 等待几分钟（GitHub 需要一点时间来部署），然后在浏览器打开 `https://owl-susan.github.io`

  ​

#### ***卡住时刻！：

创建了仓库，但是还没有网站内容，要先配置一下，ai说黄吧文件推上去是不会自动变成网站的，必须手动开启！需要在GitHub网页端开启pages功能

settings-pages-source-build and development

​                          -branch-main

​                          -folder-/root

但是不出意外的话，就出现意外了。。。。。。这时我发现branch里面只有none

why？

ai说【超严肃】：出现这种情况，**不是你操作错了，而是你的仓库现在是“空”的** —— 虽然你之前在 GitHub Desktop 里提交了文件，但**那些文件并没有真正推送到 GitHub 的远程仓库**！

#### 解决方案：先推送代码到远程仓库！！！

1. **打开 GitHub Desktop。**
2. **确保你当前在 `master`分支（左上角显示 “Current branch: master”）。**
3. **点击顶部工具栏的 Publish branch 按钮（或者如果它变成了 `Push origin`，就点那个）。**
4. **等待推送完成。你会看到左下角的 “Fetching...” 变成 “Synced” 或 “Pushed”。**

原因在于。。。因为你之前在 GitHub Desktop 里虽然点了 “Commit to master”，但那只是**本地提交**。要真正让 GitHub 看到你的代码，必须执行 **Push** 操作。就像你写好了信（Commit），但还没寄出去（Push），邮局（GitHub）当然收不到。



好吧好吧.................



接下来我打开命令行（Repository-> Open in Command Prompt）

强制把本地仓库和云端仓库绑在一起（git remote set-url origin https://github.com/owl-susan/owl-susan.github.io.git）



这时候发现我还没有一个初始文档（没有main的分支）

解决方案：

echo "# My Blog" > README.md
git add .
git commit -m "First commit"

再推送！

git branch -M main
git push -u origin main（这个时候报错是因为打不开GitHub了QAQ多试几次就好了）

然后冒出来一个窗口！登录GitHub账号！同意Git Credential Manager访问账号，帮我传代码（这时候终于知道之前装那个有什么用了！：）

然后成功出现一个页面，但还不是hugo的那个！【气】



**要想把hugo的blog完整放进去还得有下面几个步骤！**

**第一步：配置自动化部署**

你需要创建一个工作流文件，让 GitHub 每次收到推送都自动运行 Hugo。

- **创建目录**：在博客根目录新建 `.github\workflows`文件夹。
- **新建文件**：在里面创建 `hugo.yaml`。
- **填入代码**：把下面的配置复制进去（略）

**第二步：忽略本地生成文件**

本地运行产生的临时文件不需要推送到仓库。

在博客根目录创建 `.gitignore`文件，填入以下内容：（略）

 **第三步：推送到 GitHub**

确保你的仓库名符合 GitHub Pages 规范（如 `你的用户名.github.io`）。

然后在 CMD 中依次执行以下命令：

cd D:\project\Obsidian-Hugo\myBlog
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/你的用户名/你的仓库名.git
git push -u origin main

这样所有文件都传上去了！



虽然代码已经上传，但你的博客**还不能直接访问**，因为 GitHub Actions 需要时间来构建和部署。

还需要。。。。。。

**第一步：去 Actions 页面等待构建完成**

1. 在你的仓库页面（`owl-susan.github.io`），点击顶部菜单栏的 **Actions** 标签。
2. 你会看到一个正在运行的工作流（通常会显示一个黄色的圆圈或进度条）。
3. 等待它变成绿色的勾 ✅（通常需要 1~3 分钟）。

**第二步：访问你的博客**

当 Actions 显示绿色勾 ✅ 后：

1. 打开浏览器，访问：**https://owl-susan.github.io**
2. 你应该能看到你的 Hugo 博客首页了！

这个时候在actions上面我又出错了QAQ导致工作流文件的语法格式错误！

GitHub Actions 的 `workflow`文件（YAML 格式）对**环境变量/参数的写法**有严格要求。你当前的 `hugo.yaml`中，`HUGO_VERSION`的赋值方式可能用了**错误的语法**（比如缺少引号、或格式不符合 YAML 规范）

version后面的填写为”空格＋”0.163.3“

这时候重新推送便好了！

可以在blog中在美观美观

## yeah~~~

## 结束！撒花！！！！

## 太开心了！

特别鸣谢：

[Hugo 安装保姆级教程（搭建个人blog）-CSDN博客](https://blog.csdn.net/m0_59176231/article/details/148050454)

元宝