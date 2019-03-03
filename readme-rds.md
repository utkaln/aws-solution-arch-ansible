## Connect from mac

export PATH=${PATH}:/usr/local/mysql/bin

mysql -h utkallearnrdsmysql.cmdswimbn7l9.us-east-2.rds.amazonaws.com -P 3306 -u root -p

#### Connect to EC2

ssh -i "unayak-webserver-rds.pem" ec2-user@ec2-18-221-76-249.us-east-2.compute.amazonaws.com

sudo yum update -y

sudo yum install -y httpd24 php56 php56-mysqlnd

#### start webserver
sudo service httpd start

sudo chkconfig httpd on




