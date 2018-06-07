---
layout: post
author: alamoy
title: 第一篇博客,记录一下博客的入坑过程
category: Tech
tag: []
---

今天2018年6月7号，一个特殊的日子哈哈。正好我也参考教程凑活搭起来了一个小博客，虽然还有许多问题，但还是把我的心酸路程做个记录:)

1.github的使用：最开始的repo(wnzhyee.github.io)是直接从github上clone下来的，所以直接用git add/commit/push没什么问题。但之后过了一个晚上，再直接git push的时候会报错，需要用git remote远程连接上github上的repo(详情参考https://blog.csdn.net/dengjianqiang2011/article/details/9260435)

2.关于移植别的主题的步骤：
1)首先Fork或Download一份本项目代码。
2)修改_config.yaml及about.md文件，以变更个人信息。
3)修改_include目录下相关文件，以配置网站统计(analytics.html)，网友评论(comment.html)，右侧栏目(categories.html),热门文章(hot.html),友情链接(links.html)等。
4)修改CNAME文件，以绑定自己的域名。
5)删除_posts下文章，换成你自己的。
6)去谷歌自定义搜索新建一个你的搜索引擎，把你的Id替换根目录下search.html我的ID
7)最后，push到你自己的博客Repo~

3.直接Copy下来的主题，只会显示文字，不显示格式(样图)

4.关于Markdown语法:https://www.appinn.com/markdown/

