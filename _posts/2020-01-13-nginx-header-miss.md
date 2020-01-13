# 解决nginx 转发丢失header 问题

使用nginx做负载均衡或http代理时，碰到http header不转发的问题，解决方法为：

```yml
 # 配置中http部分
 underscores_in_headers on;
```  

用减号-替代下划线符号_，避免这种变态问题。nginx默认忽略掉下划线可能有些原因