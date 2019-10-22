# Nginx

## How to add a site

Copy the default config file (with vim or another text editor).

Make sure the configuration is ok:
```bash
/usr/sbin/nginx -t
```

The output should be:
```bash
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

Create a symbolic link between available and enabled sites:
```bash
ln -s /etc/nginx/sites-available/[sitename] /etc/nginx/sites-enabled/[sitename]
```
This way, any modification in sites-available config file will be linked to sites-enabled.

Restart nginx to take updates in account:

```bash
systemctl restart nginx
```
