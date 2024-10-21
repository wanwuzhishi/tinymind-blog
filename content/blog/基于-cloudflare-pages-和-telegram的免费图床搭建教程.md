---
title: 基于 Cloudflare Pages 和 Telegram的免费图床搭建教程
date: 2024-10-21T15:37:05.982Z
---

# 项目地址https://github.com/MarSeventh/CloudFlare-ImgBed


‼️ **本方案基于 Cloudflare Pages 和 Telegram （文件大小不超过20MB，过大图片会自动压缩）。**



# 一，介绍

## **1.开源**

- 前端开源（可自行修改、打包使用）

## **2.炫酷的动效（**

- 流畅丝滑的过渡动画~
- 上传文件实现呼吸灯效果

## **3.人性化上传**

- 支持绝大多数常见**图片、视频、动图**等
- 支持多种上传方式（**拖拽点击、粘贴**）
- 粘贴上传支持**文件**和**URL**
- 支持批量上传（不限同时选择文件数量，但为了保证稳定性，同时处于上传状态的文件最多为10个）
- 上传显示实时上传进度
- **上传后图片无需手动点击，可直接展示在管理页面中**
- **过大图片在前端进行压缩，提升上传稳定性和加载性能**
- 支持自定义压缩质量，自定义开启前后端压缩功能

## **4.多样化复制**

- 支持**整体复制**和**单独复制**（整体复制即将所有链接通过换行串联起来后复制）
- 支持**MarkDown、HTML、BBCode和原始链接**四种格式复制
- 上传完成后直观展示四种格式链接

## **5.支持身份认证、防滥用**

- 支持Web和API**上传认证**（
- 支持访问域名限制
- 支持上传IP统计

## **6.支持页面自定义**

- 页面背景支持**单图**、**自定义多图轮播**、**bing随机图轮播**等多种模式
- 自定义图床名称和Logo
- 自定义网站标题和Icon

## **7.一些小功能**

- 支持**随机图**API，从图床中随机返回一张图片

## **8.以及原版所有特性**

> 1.无限图片储存数量，你可以上传不限数量的图片
> 
> 
> 2.无需购买服务器，托管于 Cloudflare 的网络上，当使用量不超过 Cloudflare 的免费额度时，完全免费
> 
> 3.无需购买域名，可以使用 Cloudflare Pages 提供的`*.pages.dev`的免费二级域名，同时也支持绑定自定义域名
> 
> 4.支持**图片审查** API，可根据需要开启，开启后不良图片将自动屏蔽，不再加载
> 
> 5.支持**后台图片管理**，可以对上传的图片进行在线预览，添加白名单，黑名单等操作
> 

# 二，**部署**

## 1.创建Telegram机器人得到`TG_BOT_TOKEN`

1. 向[@BotFather](https://t.me/BotFather)发送`/newbot`，按照提示输入bot的备注、用户名等信息。成功创建如图所示的红色部分为`TG_BOT_TOKEN`。
    
    ![ ](https://tuwwzs.pages.dev/file/1729154237023_Screenshot_20241017_155651_edit_574428759597799.jpg)
    
    ## 创建Telegram频道得到**`TG_CHAT_ID`**
    
    创建一个新的频道（Channel），并按下图所示将机器人加入频道
    
    ![ ](https://tuwwzs.pages.dev/file/1729154241321_Screenshot_20241017_160513_edit_574445754749303.jpg)
    
    ![ ](https://tuwwzs.pages.dev/file/1729154241183_Screenshot_20241017_160520_edit_574457710440653.jpg)
    

### 选择你刚创建的频道，授予机器人管理员权限

![](https://tuwwzs.pages.dev/file/1729154244368_Screenshot_20241017_160533_edit_574471031884085.jpg)

## 向[@VersaToolsBot](https://t.me/VersaToolsBot)**转发**一条第2步新建频道中的消息，获取`TG_CHAT_ID`（频道ID）


‼️ **频道ID前有个负号不要忘了!!**



![](https://tuwwzs.pages.dev/file/1729154245823_Screenshot_20241017_161503_edit_574486968755694.jpg)

## 部署于Cloudflare

依托于CF的强大能力，只需简单几步，即可部署本项目，拥有自己的图床。

1. Fork https://github.com/MarSeventh/CloudFlare-ImgBed

![](https://tuwwzs.pages.dev/file/1729153327657_Clip_2024-10-17_16-21-51.png)

1. 打开 [Cloudflare Dashboard](https://dash.cloudflare.com/)，进入 Pages 管理页面，选择创建项目，选择`连接到 Git 提供程序`

![](https://alist.sanyue.site/d/imgbed/202407201047300.png)

1. 按照页面提示输入项目名称，选择需要连接的 git 仓库，点击`部署站点`
2. 将前面获取的`TG_BOT_TOKEN`和`TG_CHAT_ID`分别添加到环境变量中，对应**环境变量名为`TG_BOT_TOKEN`和`TG_CHAT_ID`**
3. **绑定KV数据库**：
    - 创建一个新的KV数据库
        
        
        ![](https://tuwwzs.pages.dev/file/1729153507708_Clip_2024-10-17_16-24-57.png)
        
    - 进入项目对应`设置`>`函数`>`KV 命名空间绑定`>`编辑绑定`>`变量名称`，填写`img_url`，KV命名空间选择刚才创建好的KV数据库
4. `重试部署`，此时项目即可正常使用