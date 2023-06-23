# Reverse Proxy Usecase
## 1. Truy cập nhiều host từ một proxy server
-  Topology:
    - Tại proxy server có chứa hai thư mục web là `example1.com` và `example2.com`.
    - Từ Client cần truy cập 2 thư mục trên thông qua 2 tên miền là *example1.com* và *example2.com*
![noimg](https://github.com/hoangbuii/helloCloud/blob/main/Month2Week3/nginximg/topouse1.png)
- Các file tại `/var/www/html` có dạng như sau:
```bash
.
├── example1.com
│   └── index.html
└── example2.com
    └── index.html
```
- File `index.html` tại `example1.com/` (`example2.com/` tương tự)
```html

<!DOCTYPE html>
<html>
<head>
  <title>HTML page from proxy server</title>
</head>
<body>
  <h1>Welcome Web page form <b>example1</b> on <i>192.168.68.170</i></h1>

  <p>This is infomation of system.</p>

  <ul>
    <li>Ubuntu</li>
    <li>NGinX</li>
    <li>Virtualization using VMware</li>
  </ul>

</body>
</html>
```
- Cấu hình NGinX: Truy cập file `/etc/nginx/nginx.conf` và thêm 2 khối server sau:
```conf
server {
    listen 80;
    server_name example1.com;
    location / {
        root /var/www/html/example1.com;
        index index.html;

        }
    }
    server {
        listen 80;
        server_name example2.com;
        location / {
            root /var/www/html/example2.com;
            index index.html;

            }
        }

```
- Khởi động lại NGinX:
```bash
sudo service nginx reload
```
- Kiểm tra kết quả: 
    - Khi truy cập tên miền *example1.com* tại client sẽ truy cập đến host tại `/var/www/html/example1.com`
    - Khi truy cập tên miền *example2.com* tại client sẽ truy cập đến host tại `/var/www/html/example2.com`
    ![noimg](https://github.com/hoangbuii/helloCloud/blob/main/Month2Week3/nginximg/webonpro1.png)
    ![noimg](https://github.com/hoangbuii/helloCloud/blob/main/Month2Week3/nginximg/webonpro2.png)
