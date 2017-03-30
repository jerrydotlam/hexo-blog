---
title: Nice to see hexo
date: 2017-03-30 15:38:51
tags: hexo
---

### 很高兴遇见`hexo`这货。

#### 其实说白了是很高兴自己又一次的把个人博客给弄起来，无论前面停掉了多少次，每次都能不厌其烦的找到一种自认为靠谱的方式重新建立起来。无论这次能坚持多久，但这颗不忘留下点什么的心，总是让自己敬佩的，呵呵。

`hexo`是`nodejs`实现的静态文档生成工具，类似于`jekyll`。这也刚好是我一直想去做的事情。搭建`hexo`对懂node的开发人员来说简单易上手，只需要遵循官方网站的说明，就可以很容易配置一个漂亮的个人博客。我是一眼看中了[Tranquilpeak](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak)这个主题，虽然安装过程出了一些小问题，但对艺术有追求的码农来说，这都不是事，将安装过程中的问题大概总结如下：

+ **问题：安装主题`tranquilpeak`，出现安装失败，无法下载`node-sass`相关的文件**

```
    Cannot download "https://github.com/sass/node-sass/releases/download/v3.13.1/win32-x64-51_binding.node"
```

解决：直接打开这个链接地址会重定向到AWS的服务去，很明显是被墙掉了，可以通过淘宝镜像单独安装`node-sass`来解决这个问题：

```
    npm install node-sass --sass-binary-site=https://npm.taobao.org/mirrors/node-sass/
```

淘宝的镜像真是贡献巨大，NPM遇到的大部分网络问题都可以通过它来解决。

+ **问题：在主题下面无法执行lint。这个算不上问题，原主题作者的代码没通过`eslint`校验，根据提示修改源代码即可**

+ **问题：无法执行hexo命令，提示找不到`../highlight_alias.json`**

```
ERROR Script load failed: themes\tranquilpeak\scripts\tags\tabbed_codeblock.js
Error: Cannot find module '../highlight_alias.json'
    at Function.Module._resolveFilename (module.js:470:15)
```

解决：修改`tranquilpeak`的package.json文件，将`hexo-util`升级到0.6.0以上。

中间还有一些`hexo`本身的问题，可直接参考[Trouble Shooting](http://hexo.io/docs/troubleshooting.html)修改即可。

安装完后，如果要在两个以上的机器编辑内容怎么办？或者将hexo部署到某个云服务器，但是又不能在云服务器上直接写。这时可以将`hexo`整个放到github上，然后在任何地方都可以通过clone这个库来进行内容编辑了。这里只需要完成几个简单配置即可：

1. 将`hexo`的基础文件同步到github（[查看我的](https://github.com/jerrydotlam/hexo-blog)）
2. 主题类安装包也可以直接安装后同步，或者使用Git Submodule的方式进行安装
3. 主题包里有涉及到自定义修改的内容，比如`_config.yml`配置或一些文件，可单独配置一个目录，在同步安装的时候覆盖掉主题包原来的内容即可；或者更直接的方式，从主题包的github上拉出新分支，将内容修改为自己想要的（高度定制化主题包），然后在使用Git Submodule的方式来进行维护
4. 后续所有文章发布，甚至是只需要同步`public`目录即可
