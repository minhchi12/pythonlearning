######Trên HĐH CentOS, muốn kiểm tra dịch vụ httpd (Apache) có hoạt động hay không, thực hiện như sau: tạo file checkhttp.py có nội dung như bên dưới, tại thư mục chứa file, tiến hành chạy file bằng câu lệnh #python checkhttp.py

<code>import commands
output = commands.getoutput('ps -A')
if 'httpd' in output:
        print("Httpd is up and running!")</code>
