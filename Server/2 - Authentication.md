# Lab 1

Use Intruder with the user names as the payload sets and add the "Incorrect username" in the Intruder->Options->Grep - Match.

After that use the password payload set and add the "Incorrect password" string to get the successful login

# Lab 2

Use the Intruder->Options->Grep - Extract - in order to .

# Lab 3

Use the Intruder to find the response time for the given user with a wrong password - note that time,

Use the Intruder to find the response time for the other users (with the candidate list) then find the user with the closest response time to the given user. Repeat this process a few times to verify and then use the Intruder with this user to brute force the password (you should recieve 302 on the correct password)

# Lab 4

This requires two sets of payloads, one with alternating names of carlos and weiner, the other is alternation between peter and passwords,

then use the Intruder to attack using these two dicts to find carlos's password (should be with 302 status code)


# Lab: 2FA simple bypass

enter Carlos credentials and just jump to the home page after you got to the next factor authentication page

# Lab: 2FA broken logic

The key here is to use the second stage of the two factor authentication of wiener to brute force carlos's authentication code (by changng "verify" in cookies and using Intruder)

# Lab: Brute-forcing a stay-logged-in cookie

After authenticating as wiener we can see that the response from the server set the cookie to:
```
stay-logged-in=d2llbmVyOjUxZGMzMGRkYzQ3M2Q0M2E2MDExZTllYmJhNmNhNzcw
```
which is base64 of:
```
wiener:51dc30ddc473d43a6011e9ebba6ca770
```

We can identify that the latter (after the username) is MD5 hash, possibly for the password for weiner, now we will use the request:
```http
GET /my-account HTTP/1.1
Host: aced1f021fe7a8318022593e00d9000f.web-security-academy.net
Cookie: stay-logged-in=d2llbmVyOjUxZGMzMGRkYzQ3M2Q0M2E2MDExZTllYmJhNmNhNzcw; session=tudvBq62ELO1glvnWxA1k3NLSO3qxTGb
```

For our brute force Intruder attack where we will enumerate on the stay-logged-in cookie where the payload set is (psuedo code):
```
encode_base64(carlos:MMD5(password)) --> for every password in the original set
```

# Lab: Password reset broken logic

The way we change carlos's password is we go all the way of resetting wiener's password and for the final request with the new password, we switch the namme of the username to carlos *while we still have the temporary user token*.
This resets carloses password
