---
title: 宝塔申请 SSL 出现域名待验证
abbrlink: 4659
date: 2021-12-15 00:00:00
categories:
  - 问题
tags:
  - 宝塔
  - SSL
---

# 宝塔申请 SSL 出现域名待验证

## 写在前面

宝塔面板非常方便，其中免费的 SSL 一键申请部署也很方便，但是申请的时候经常莫名其妙出现**域名待验证**，并且有时候过很久都不通过。

## 场景

使用宝塔面板申请 SSL 证书的时，填写信息并提交资料，域名后面显示域名待验证。

### 原因

申请证书的验证方式有两种：FILE 验证与 DNS验证。

从宝塔面板中直接申请，用的是 FILE 验证，**这种验证方式有时候比较慢**，这时，可以直接登录 https://www.bt.cn，在 SSL 管理中申请证书，用 DNS 验证。

### 解决方法

DNS 验证需要按照要求，去域名解析的平台添加一条 **TXT 记录**。

完成后在命令行检验 TXT 记录是否生效。

```sh
nslookup -qt=TXT yourdomain.com
```

若生效，会显示解析结果。若不生效，就要检查一下是否有相同的 **CNAME** 记录。 因为同名的 **CNAME** 记录与 **TXT** 记录是会冲突的。

为不影响 **CNAME** 的使用，可以先将 **CNAME** 记录改为 **A** 记录，等确认 **TXT** 记录解析生效后，去服务器的宝塔后台验证域名，通过验证后再改回来即可。

