# Redirect from http to https automatically

> from [here](http://www.allcloud.io/how-to/how-to-force-https-behind-aws-elb/) and added my notes.

### Nginx

```
server {
  listen 80;
  ....
  location / {
    if ($http_x_forwarded_proto != 'https') {
      rewrite ^ https://$host$request_uri? permanent;
    }
  ....
  }
}
```

`http_x_forwarded_proto` header is from AWS ELB. And use `return 301 https://$host$request_uri;` works as well.

### Apache

```
<VirtualHost *:80>
...
RewriteEngine On
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteRule ^.*$ https://%{SERVER_NAME}%{REQUEST_URI}
...
</VirtualHost>
```

### IIS(Windows)

Install IIS Url-Rewrite module, using the configuration GUI add these settings

```
<rewrite xdt:Transform="Insert">
<rules>
<rule name="HTTPS rewrite behind ELB rule" stopProcessing="true">
<match url="^(.*)$" ignoreCase="false" />
<conditions>
<add input="{HTTP_X_FORWARDED_PROTO}" pattern="^http$" ignoreCase="false" />
</conditions>
<action type="Redirect" redirectType="Found" url="https://{SERVER_NAME}{URL}" />
</rule>
</rules>
</rewrite>
```
