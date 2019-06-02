#Paste the following to Bootstrap Script

yum update -y
yum install httpd -y
service httpd start
chkconfig httpd on
cd /var/www/html
echo "<html><h1>This is Utkal's WebServer 01</h1></html>" > index.html

