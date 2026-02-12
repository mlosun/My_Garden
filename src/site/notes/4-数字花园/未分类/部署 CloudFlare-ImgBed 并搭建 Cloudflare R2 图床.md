---
{"dg-publish":true,"dg-path":"未分类/部署 CloudFlare-ImgBed 并搭建 Cloudflare R2 图床.md","permalink":"/未分类/部署 CloudFlare-ImgBed 并搭建 Cloudflare R2 图床/","created":"2026-02-04","updated":"2026-02-12"}
---


## 方案简介

[CloudFlare ImgBed](https://github.com/MarSeventh/CloudFlare-ImgBed) 是一个能够基于 Cloudflare 生态构建图床的开源项目，充分利用了 Cloudflare 提供的免费计划，搭建一个具有上传、管理、读取、删除的全链路文件托管解决方案。其中：
- Cloudflare Pages 提供项目托管，支持绑定域名
- Cloudflare Works KV 提供项目配置
- Cloudflare R2 提供对象存储（需要绑定支付方式，但在免费额度内不扣费）

基于 Cloudflare 免费计划提供的额度，对于个人用户已经足够使用，且在国内拥有还不错的访问速度，可以说这个方案是目前搭建个人图床的最佳方案了。

## 部署 CloudFlare ImgBed

1. 访问 [CloudFlare ImgBed 项目](https://github.com/MarSeventh/CloudFlare-ImgBed)，Fork 到自己的 Github 仓库
2. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)，进入 Workers 和 Pages 页面
3. 创建一个 Pages 项目，导入刚才 Fork 的仓库
4. 项目设置如下：
   - 项目名称：`cloudflare-imgbed`
   - 生产分支`main`
   - 构建命令：`npm install`
   - 构建输出目录：`/`
5. 保存并部署即可

## 创建 Cloudflare Workers KV 并绑定

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)，进入 Workers KV 页面
2. 创建一个命名空间，命名为`img_url`
3. 返回刚创建的 Pages 项目，进入设置页面，添加绑定一个 KV 命名空间
4. 绑定刚创建的命名空间，变量名称`img_url`


## 创建 Cloudflare R2 并绑定

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)，进入 R2 对象存储页面
2. 创建一个存储桶，命名为`img_r2`
3. 返回刚创建的 Pages 项目，进入设置页面，添加绑定一个 R2 存储桶
4. 绑定刚创建的存储桶，变量名称`img_r2`

## 重新部署并设置管理员账户

1. 返回刚创建的 Pages 项目，进入部署页面
2. 找到最新的部署记录，重新部署一次
3. 等待部署完成后，就可以通过 Pages 提供的域名访问图床了
4. CloudFlare ImgBed 项目的管理后台默认无需密码，部署后需及时设置

## 其他补充说明

#### 关于绑定域名

仅需绑定自定义域名到 Pages 项目即可（设置 CNAME 记录即可），无需绑定域名到 R2 存储桶。

如果要 R2 存储桶直接绑定自定义域名，则需要将域名的 DNS 托管给 Cloudflare 才可以。

## 参考资料
- [CloudFlare ImgBed 项目](https://github.com/MarSeventh/CloudFlare-ImgBed)
- [CloudFlare ImgBed 文档](https://cfbed.sanyue.de/)
- [为什么用 S3 (R2)?](https://yfi.moe/post/manage-website-images#%E4%B8%BA%E4%BB%80%E4%B9%88%E7%94%A8-s3-r2)
