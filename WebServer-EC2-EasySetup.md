yum install httpd -y
chkconfig httpd on
service httpd start
cd /var/www/html
vi index.html
#[INSERT]
<html><h1> Text goes here </h1></html>
