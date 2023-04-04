---
title: Hexo主题butterfly
cover: "pexels-forest.png"
categories: 
	-教程
---

## butterfly主题

Hexo官方网站有很多精美的[主题](https://hexo.io/themes/)，安装都比较简单，但是比较麻烦的就是主题的配置。

本篇文章介绍的是butterfly主题，但是不再赘述相关安装问题，而是会列出部分butterfly主题安装的相关配置问题。



## 主题配置文件

为了减少升级主题后带来的不便，请使用以下方法（建议，可以不做）。

在 hexo 的根目录创建一个文件 _config.butterfly.yml，并把主题目录的 _config.yml 内容复制到 _config.butterfly.yml 去。( 注意: 复制的是主题的 _config.yml ,而不是 hexo 的 _config.yml)

注意： 不要把主题目录的 _config.yml 删掉

注意： 以后只需要在 _config.butterfly.yml进行配置就行。
如果使用了 _config.butterfly.yml， 配置主题的 _config.yml 将不会有效果。

Hexo会自动合併主题中的_config.yml和 _config.butterfly.yml里的配置，如果存在同名配置，会使用_config.butterfly.yml的配置，其优先度较高。

强烈建议执行上述步骤，在之后的升级主题的时候，就不会导致更新将原有的配置覆盖！

## 导航菜单相关问题

导航菜单指的是网页右上角的菜单栏，如下图所示。

![image-20230403233240202](HexoTheme/image-20230403233240202.png)

相关配置：
```yaml
Home: / || fas fa-home
Archives: /archives/ || fas fa-archive
Tags: /tags/ || fas fa-tags
Categories: /categories/ || fas fa-folder-open
List||fas fa-list:
 Music: /music/ || fas fa-music
 Movie: /movies/ || fas fa-video
Link: /link/ || fas fa-link
About: /about/ || fas fa-heart
```

其中Home这些冒号前的都是可以写成中文的，例如

```yaml
主页: / || fas fa-home
```

这里比较难以理解的可能就是图标问题，butterfly支持font-awesome v6图标，你可以在这个[网站](https://fontawesome.com/)中获取到你想要的图标的名称。

## 打字机设置

一开始看yaml的文件描述不是很清晰，尝试多次后未果，最后还是去网上搜了一下才知道格式，配置如下：

```yaml
subtitle:
  enable: true                    	#是否显示subtitle
  # Typewriter Effect (打字效果)
  effect: true						#是否开启打字机效果
  # Customize typed.js (配置typed.js)
  # https://github.com/mattboldt/typed.js/#customization
  typed_option:
  # source 調用第三方服務
  # source: false 關閉調用
  # source: 1  調用一言網的一句話（簡體） https://hitokoto.cn/
  # source: 2  調用一句網（簡體） https://yijuzhan.com/
  # source: 3  調用今日詩詞（簡體） https://www.jinrishici.com/
  # subtitle 會先顯示 source , 再顯示 sub 的內容
  #source: true
  source: false					#是否调用第三方服务，从接口处获取语句
  #subtitle: "This a line。"
  # 如果關閉打字效果，subtitle 只會顯示 sub 的第一行文字
  sub: 							#多行是随机
    - 人生就是一场没有终点的旅行
    - 爱别人首先要爱自己
```

