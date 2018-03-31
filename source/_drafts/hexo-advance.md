---
title: hexo-advance
tags:
categories:
keywords:
---
# 站点图标

站点图标[NexT主题个性化设置 | Jey Zhang](http://www.jeyzhang.com/next-theme-personal-settings.html)
[制作ico图标 | 在线ico图标转换工具 方便制作favicon.ico - 比特虫 - Bitbug.net](http://www.bitbug.net/)
```yml
favicon:
  medium: /images/favicon.ico
```

# 打赏功能

[打赏功能](http://theme-next.iissnan.com/theme-settings.html#reward)

```yml
# Reward
reward_comment: 写得不错，发张奖状
wechatpay: /images/wechatpay.jpg
alipay: /images/alipay.jpg
```

打赏字体不闪动
修改文件next/source/css/_common/components/post/post-reward.styl，然后注释其中的函数wechat:hover和alipay:hover，如下：

```styl
/* 注释文字闪动函数
 #wechat:hover p{
    animation: roll 0.1s infinite linear;
    -webkit-animation: roll 0.1s infinite linear;
    -moz-animation: roll 0.1s infinite linear;
}
 #alipay:hover p{
   animation: roll 0.1s infinite linear;
    -webkit-animation: roll 0.1s infinite linear;
    -moz-animation: roll 0.1s infinite linear;
}
*/
```

# 分享

[theme-next/theme-next-needmoreshare2: NeedMoreShare2 for NexT.](https://github.com/theme-next/theme-next-needmoreshare2)，支持HTTPS，JiaThis不支持HTTPS。

# 评论系统

多说替代评论系统方面，多说挂了，推荐用来必力，若不被墙，Disqus是首选。[参考多说替代方案](https://www.zhihu.com/question/57426274/answer/153891650)
[友言 - 专业网站社会化评论系统](http://www.uyan.cc/)


# 阅读数

……