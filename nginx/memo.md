# Nginx
## Allow access from specific segments
[Refs](http://nginx.org/en/docs/http/ngx_http_access_module.html)

```
location / {
  deny  192.168.1.1;
  allow 192.168.1.0/24;
  allow 10.1.1.0/16;
  allow 2001:0db8::/32;
  deny  all;
}
```
