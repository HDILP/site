前言：

哈哈哈咕了好几个星期终于更了！

刚刚把我的blog的主题代码pull了一下同步到最新（我改了一些文件，出现了冲突。解决方法：`git add .` `git commit -m "1"`之后再`git pull`），又把网站评论系统Twikoo更新了一下（其实更新主题就把前端更了，后端只要改一下版本号就会自动更新了，很方便），现在准备把blog从**GitHub Page**迁移到**Vercel**。因为GitHub Page套Cloudflare对于国内来说实在是<u>太慢了</u>。

------

首先先在GitHub上新建一个repo，把这个repo用**GIt**连接到Hexo根目录（在`hexo init`的时候就已经帮你把**.git文件夹**和其他的东西弄好了）。

![add new repo](https://pic.imgdb.cn/item/6619329168eb935713c570c3.png)

之后直接`git add .` `git commit -m "first commit"` `git push -u origin main `组合技

之后打开你的**vercel**，把**刚在github新建的repo**添加进去（首页 - Add New... - Project - Import Git Repository那里选择你的Repo）。然后它就会自动开始编译。

之后遇到了一个坑（满屏红字警告）

![](https://pic.imgdb.cn/item/6619374968eb935713cbd57d.png)

看上去是一篇文章的内容出了问题。

~~原因（机翻）：~~

> ~~Hexo 使用 [Nunjucks] 来渲染帖子（旧版本中使用 [Swig]，其语法相似）。用`{{ }}`或包裹的内容`{% %}`将被解析并可能导致问题。~~

~~之后直接三个反引号过去之后编译过了，但文件空的（6666666666666），发现远程仓库主题文件夹空的………………~~

**真实原因：有一篇文章使用了主题中的标签，但主题被设置成了子模块（使用`git clone`安装模块导致的），git push的时候不会把主题文件夹推送到远程库中，编译器无法识别这个东西，所以出现了报错。**

解决方式：

> 若采用 `git clone` 的方式安装了主题，需要在 `commit` 之前，把主题文件夹里面的 `.git` 重命名或者删除。否则会出现远程仓库中，主题文件夹空白的情况。

但如果删掉.git文件夹，后续就不能`git pull`更新了，所以就把整个hexo根目录复制到另一个文件夹，在那个新文件夹删.git。

累了，明天再写（23333333333333）

------

4-13更新：

删掉之后还要清空暂存区的内容`git rm --cached <file>`，之后直接`git add .` `git commit -m "second commit"` `git push -u origin main `组合技。之后vercel就会自动开始编译。编译过了之后把最新Deployments的设置成生产（点击**Promote to Production**），

![](https://pic.imgdb.cn/item/661a5f2b68eb9357136b3e94.png)

最后分配域名。我们的网站迁移就成功了！

最后的成果：

![](https://pic.imgdb.cn/item/661b708868eb935713c1a8d2.png)

![](https://pic.imgdb.cn/item/661b709868eb935713c1c2eb.png)

![这神一般的速度啊](https://pic.imgdb.cn/item/661b710b68eb935713c3e37f.png)

（以前用CloudFlare的时候至少用50秒……）

好了，这一期就到此结束啦！o(〃＾▽＾〃)o，感谢大家的观看，我们下期再见！拜拜！



下期预告：使用WordPress搭建PHP动态网站（我这个是静态的）