# mutillidae

## A1 - Injection

### SQLi - Extract Data

#### User Info

![user info](assets/mutillidae/sqli1.png)

* the `Name` textbox can contain literally any word
* the `Password` textbox can be `' OR '1'='1`
* this will display the Username, Password and Signature of all the users in the db
* implies that the sql query is something similar to `SELECT * FROM owasp10.accounts WHERE Username='$USERNAME' AND Password='$PASSWORD'`
* so the bypassed query will look like `SELECT * FROM owasp10.accounts WHERE Username='abc' AND Password='' OR '1'='1'`
* this will be equivalent to `SELECT * FROM owasp10.accounts`

### SQLi - Bypass Authentication

#### Login

* to exploit this and login as `admin`, the `Name` can be `admin`
* the `Password` field can be `' OR '1'='1`
* a non-null return value to the sql query (bypass too) which must be similar to [User Info](#user-info) will be expected

### SQLi - Insert Injection

#### Register

judging the information asked or by breaking the sql query with just `'` as the username, we can come to know that the actual sql query is

```sql
INSERT INTO accounts (username, password, mysignature) VALUES ('$USERNAME', '$PASSWORD', '$SIGNATURE')
```

since none of the fields are compulsory, we inject sql in just the username textbox to get the mysql admin password with `abc', 'abc', (SELECT password FROM mysql.user WHERE user='admin'))#`

while the injected sql query got executed, i could not see the mysql admin password and i'm not sure why :-(

### Blind SQL via Timing

#### Login

#### User Info

### SQLMAP Practice Target

#### View Someones Blog

starting from scratch, i first ran sqlmap with `sqlmap -u "http://MACHINE_IP/mutillidae/index.php?page=view-someones-blog.php" --cookie "PHPSESSID=fdbcb501dbfb4c396f0a7315135ae707" --dbms mysql --method POST --data "author=john&view-someones-blog-php-submit-button=View+Blog+Entries" --current-db` to retrieve info about the current database and then i ran `sqlmap -u "http://MACHINE_IP/mutillidae/index.php?page=view-someones-blog.php" --cookie "PHPSESSID=fdbcb501dbfb4c396f0a7315135ae707" --dbms mysql --method POST --data "author=john&view-someones-blog-php-submit-button=View+Blog+Entries" -D owasp10 --all` to fetch all information possible

#### User Info

### HTML Injection (HTMLi)

#### Add to your blog

### HTMLi via HTTP Headers

#### HTTP Response Splitting (Hint: Difficult)

### HTMLi Via DOM Injection

#### HTML5 Storage

### HTMLi Via Cookie Injection

#### Capture Data Page

### Command Injection

#### DNS Lookup

### JavaScript Injection

#### Those "Back" Buttons

#### Password Generator

### HTTP Parameter Pollution

#### Poll Question

### Cascading Style Injection

#### Set Background Color

### JavaScript Object Notation (JSON) Injection

#### Pen Test Tool Lookup

## A2 - Cross Site Scripting (XSS)

### Reflected (First Order)

#### DNS Lookup

a simple `<script>alert()</script>` in the **Hostname/IP** textbox will be enough

#### Pen Test Tool Lookup

#### Text File Viewer

#### User Info

#### Set Background Color

#### HTML5 Storage

#### Capture Data Page

### Persistent (Second Order)

here, the xss attack is stored in the db and so, the attack is executed everytime the messages are rendered

#### Add to your blog

![blog stored xss](assets/mutillidae/xss1.png)

the good ol `<script>alert()</script>` will be enough to xss the website

#### View someone's blog

### DOM Injection

#### HTML5 Storage

### Via "Input" (GET/POST)

#### Add to your blog

#### View someone's blog

#### Text File Viewer

#### DNS Lookup

#### User Info

#### Missing HTTPOnly Attribute

#### Set Background Color

#### Pen Test Tool Lookup

### Via HTTP Headers

#### Browser Info

#### Those "Back" Buttons

### Via Misconfiguration

#### Missing HTTPOnly Attribute

### Against HTML 5 Storage

#### HTML5 Storage

Against JSON

Pen Test Tool Lookup

### Via Cookie Injection

#### Capture Data Page

## A3 - Broken Authentication and Session Management

#### Cookies

#### Login

## A4 - Insecure Direct Object References

#### Text File Viewer

#### Source Viewer

#### Credits

#### Cookies

#### Arbitrary File Inclusion

* the `page` query string in the URL seems to be exploitable - `http://MACHINE_IP/mutillidae/index.php?page=arbitrary-file-inclusion.php`
* so, we can access the `/etc/passwd` file by manipulating the URL parameters like `http://$MACHINE_IP/mutillidae/index.php?page=/etc/passwd`

## A5 - Cross Site Request Forgery (CSRF)

#### Add to your blog

#### Register User

## A6 - Security Misconfiguration

#### Directory Browsing

* as seen in [robots.txt](#robots.txt), some directories can be browsed without restriction
* for example, `http://MACHINE_IP/mutillidae/passwords/` has directory listing enabled

#### GET for POST

## A7 - Insecure Cryptographic Storage

#### User Info

#### HTML5 Storage

## A8 - Failure to Restrict URL Access

#### "Secret" Administrative Pages

* the page in question is `phpinfo.php`
* the actual contents of `phpinfo.php` is

```php
<?php

phpinfo();

?>
```

* in some cases, the contents of this page has been used to determine the PHP version and if it is vulnerable

#### Robots.txt

![robots.txt](assets/mutillidae/robots.png)

* `robots.txt` seems to contain some sensitive directories
* probably the right way to achieve this effect would be through the use of `.htaccess`? [Research needed]

## A9 - Insufficient Transport Layer Protection

#### Login

#### User Info

## A10 - Unvalidated Redirects and Forwards

#### Credits

* the hyperlinks in the page are of the format - `http://MACHINE_IP/mutillidae/index.php?page=redirectandlog.php&forwardurl=$REDIRECT_TO_URL`
* this feature can be exploited by changing the `forwardurl` query value since the redirect link is not validated

#### Setup/reset the DB (Disabled: Not Admin)

## Others

### OWASP 2007 A3 - Malicious File Execution

#### Text File Viewer

#### Source Viewer

### OWASP 2007 A6 - Information Leakage and Improper Error Handling

#### Cache Control

#### X-Powered-By HTTP Header

#### HTML/JavaScript Comments

#### Click-Jacking

#### Cross-Site Framing (Third-Party Framing)

#### HTML5 Storage

### Denial of Service

#### Text File Viewer

### JavaScript "Security"

#### Login

#### Add to your blog

#### HTML5 Storage

### Data Capture Pages

#### Data Capture

#### View Captured Data
