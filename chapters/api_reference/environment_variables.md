# Environment variables

Everytime an app is launched it receives a set of environment variables to work with. They are all accesible as `process.env['<variable-name']` or `process.env.<variable-name>`

```
APP_PORT # assigned randomly, starts from port 3000
APP_NAME # the name appearing in your app's package.json

NETBEAST # Netbeast first public IP and port
         # 192.168.1.32:80
```