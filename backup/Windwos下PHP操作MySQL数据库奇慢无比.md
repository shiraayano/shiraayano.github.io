# Windwos下PHP操作MySQL数据库奇慢无比问题解决

笔者写的一个 API 涉及数据库操作，延迟竟然达到了惊人的 2 秒多，放到网站上直接导致超时。

![图片](https://github.com/user-attachments/assets/5d9ac585-8223-4930-a5cc-0d83bfbe7639)

为此，笔者在 nginx、PHP、MySQL 配置中反复折腾了很久。MySQL 查询理论上是非常快的，nginx 的配置也没问题，PHP 换了几个版本还是一样。最后破案之后发现是个非常无语的事情。

## 解决方案

将 `localhost` 改为 `127.0.0.1`。

![图片](https://github.com/user-attachments/assets/73e5ad13-a200-4f80-9f95-50ff9efaa3f5)

但是，这样真的就完美解决了吗？在使用 phpMyAdmin 等工具时，默认是 `localhost`。笔者给出的折中方法是禁用 IPv6。

## 故障分析

PHP 在 Windows 中会默认将 `localhost` 解析成 IPv6 地址，如果 IPv6 配置有问题，大概率是不通的，然后再尝试 IPv4。在网上看见有人说改 hosts，笔者亲测无效，默认 hosts 配置中就有 `localhost 127.0.0.1`。PHP CGI 不会使用本地的 hosts 文件。

![图片](https://github.com/user-attachments/assets/d96de018-8fd0-4750-b037-84de6fc3a9e4)

最后，IPv6 的发展是大势所趋，但是笔者在使用过程中也遇到过一些离谱的问题，比如以前阿里云盘默认解析到 IPv6，然后无法使用之类的。
