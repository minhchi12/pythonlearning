#####Kiểm tra dịch vụ httpd trên CentOS và gởi email thông báo đến cho SysAdmin, đồng thời restart lại dịch vụ httpd nếu phát hiện dịch vụ bị off

Có thể kết hợp thêm với các thông số khai báo SMTP để kết nối đến 1 SMTP (có user/pass) - ví dụ Gmail để gởi email đi.

<pre><code>import commands
import smtplib
import subprocess

output = commands.getoutput('ps -A')
sender = 'webmaster@blogit.edu.vn'
receivers = ['webmaster@blogit.edu.vn']
message = """From: Server x.x.x.x <webmaster@blogit.edu.vn>
To: Webmaster <webmaster@blogit.edu.vn>
Subject: Server x.x.x.x is normal
Httpd is up and running
"""
message1 = """From: Server x.x.x.x <webmaster@blogit.edu.vn>
To: Webmaster <webmaster@blogit.edu.vn>
Subject: Server x.x.x.x accident
Httpd is stop
"""
if 'httpd' in output:
        smtpObj = smtplib.SMTP('localhost')
        smtpObj.sendmail(sender, receivers, message)
        print "Successful send Email"
elif 'httpd' not in output:
        smtpObj = smtplib.SMTP('localhost')
        smtpObj.sendmail(sender, receivers, message1)
        # Khởi động lại dịch vụ httpd
        subprocess.call(["service", "httpd", "restart"])
        print "Successful send Email"
else:
        print "Error: unable to send email"</code></pre>
