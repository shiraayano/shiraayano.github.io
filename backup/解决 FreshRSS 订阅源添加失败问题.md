在使用 FreshRSS 订阅 RSS 源时，我遇到了一个问题：订阅源添加失败，并且日志中提示 SSL 证书问题。经过一番折腾，终于解决了这个问题。本文将分享具体的解决过程，希望对遇到同样问题的朋友有所帮助。

## 问题描述

在 FreshRSS 中添加订阅源时，遇到了以下错误：
订阅源添加失败，检查 FreshRSS 日志 查看详情。你可以在 URL 后添加 #force_feed 尝试强制添加。

```plaintext
详细日志
⚠️ 2024-07-27 14:28:55 Unknown error for feed [https://blog.adouzi.eu.org/rss.xml]
⚠️ 2024-07-27 14:24:31 cURL error 60: SSL certificate problem: unable to get local issuer certificate [https://blog.adouzi.eu.org/rss.xml]
```

从错误信息来看，主要是由于 SSL 证书验证失败导致的。

## 解决步骤

### 1. 下载 CA 证书包

首先，需要下载最新的 CA 证书包 `cacert.pem`。这是 cURL 用来验证 SSL 证书的。

1. 打开浏览器，访问 cURL CA 证书页面：[https://curl.se/docs/caextract.html](https://curl.se/docs/caextract.html)。

2. 点击页面中的“CA Extract”或“Download CA Bundle”链接，下载 `cacert.pem` 文件。

3. 将下载的 `cacert.pem` 文件保存到一个合适的位置，例如 `C:\php\extras\ssl\cacert.pem`。

### 2. 配置 PHP 使用 CA 证书

接下来，需要配置 PHP 使用下载的 CA 证书包。

1. 打开 `php.ini` 文件，通常位于 PHP 安装目录下，例如 `C:\php\php.ini`。

2. 找到并编辑以下行：
   ```ini
   ;curl.cainfo =
   ```
   修改为：
   ```ini
   curl.cainfo = "C:\php\extras\ssl\cacert.pem"
   ```

3. 保存并关闭 `php.ini` 文件。

4. 重启你的 Web 服务器（例如 Apache 或 Nginx），使更改生效。

### 3. 强制添加订阅源

在 FreshRSS 中添加订阅源时，可以在 URL 后添加 `#force_feed`，例如：
```plaintext
https://blog.adouzi.eu.org/rss.xml#force_feed
```
这样可以强制 FreshRSS 添加订阅源。

### 4. 检查订阅源格式

确保订阅源是有效的 RSS 或 Atom 格式，可以通过在浏览器中打开订阅源 URL 来验证其格式。

## 验证

完成以上步骤后，再次尝试在 FreshRSS 中添加订阅源，问题应该已经解决。如果仍然遇到问题，可以再次查看日志，检查是否有新的错误信息。

## 结论

通过更新 CA 证书包和配置 PHP 使用正确的证书文件，成功解决了 FreshRSS 订阅源添加失败的问题。如果你也遇到了类似问题，希望这篇文章能帮到你。如果有任何疑问或进一步的问题，欢迎在评论区留言讨论。

---

这篇文章详细描述了问题解决的过程，供大家参考。如果你有其他问题或建议，欢迎随时交流！