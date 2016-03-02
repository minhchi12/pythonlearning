#####Kiểm tra dịch vụ httpd trên CentOS và gởi email thông báo đến cho SysAdmin

<pre><code>
import commands
import smtplib

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
Subject: Server x.x.x.x is accident

Httpd is stop
"""

if 'httpd' in output:
        smtpObj = smtplib.SMTP('localhost')
        smtpObj.sendmail(sender, receivers, message)
        print "Successful send Email"
elif 'httpd' not in output:
        smtpObj = smtplib.SMTP('localhost')
        smtpObj.sendmail(sender, receivers, message1)
        print "Successful send Email"
else:
   print "Error: unable to send email"
