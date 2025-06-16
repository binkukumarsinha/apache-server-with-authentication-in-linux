# apache-server-with-authentication-in-linux
## Configuration Apache Server on behalf of user  password authentication

## Install Basic Packages on Redhat based System

```shell
## BASE LIBRARIES ##
yum update -y
yum install httpd* -y
systemctl start httpd
systemctl status httpd
yum install firewalld*
systemctl restart firewalld
firewall-cmd --permanent --zone=public --add-service=httpd
firewall-cmd --reload
systemctl restart firewalld
systemctl restart httpd
```
Then just enter the ip address of the linux system into any browser.


## Change Dir to /var/www/html and create a dir name with apache. as below:
```shell
cd /var/www/html/
mkdir apache   
vi index.html
```

For user based authentication edit the 'httpd.conf' file using vi editor:
```
vi /etc/httpd/conf/httpd.conf
```
Then enter the below code:
```
<Directory "/var/www/html/apache">
	AuthType Basic
	AuthName "Authorized Users Only"
	AuthUsersFile /etc/httpd/authpass
	Require vaild-user apache
</Directory>
```
save and exit the vi editor

THEN add users for authentication 

```
useradd user1    
useradd user2
htpasswd -c /etc/httpd/authpass user1     
htpasswd -m /etc/httpd/authpass user2
```
Then need to do this steps:
```
mkdir -p /var/www/html/apache/.htaccess
vi /var/www/html/apache/.htaccess
```
add below code to /var/www/html/apache/.htaccess file
```
AuthType Basic
AuthName "Authorized Users Only"
AuthUsersFile /etc/httpd/authpass
Require vaild-user apache

```
Then restart the apache service
```
systemctl restart httpd
```




## Install Basic Packages on Debian / Ubuntu based System

```shell
## BASE LIBRARIES ##
apt-get update -y && upgrade -y
apt install apache2* -y
systemctl start apache2
systemctl status apache2
apt-get install firewalld*
systemctl restart firewalld
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --reload
systemctl restart firewalld
systemctl restart apache2
```

Then just enter the ip address of the linux system into any browser.


## Change Dir to /var/www/html and create a dir name with apache. as below:
```shell
cd /var/www/html/
mkdir apache   
vi index.html
```

For user based authentication edit the 'httpd.conf' file using vi editor:
```
vi /etc/apache2/apache2.conf
```
Then enter the below code:
```
<Directory "/var/www/html/apache">
	AuthType Basic
	AuthName "Authorized Users Only"
	AuthUsersFile /etc/apache2/authpass
	Require vaild-user 
</Directory>
```
save and exit the vi editor

THEN add users for authentication 

```
useradd user1    
useradd user2
htpasswd -c /etc/apache2/authpass user1     
htpasswd -m /etc/apache2/authpass user2
```
Then need to do this steps:
```
mkdir -p /var/www/html/apache/.htaccess
vi /var/www/html/apache/.htaccess
```
add below code to /var/www/html/apache/.htaccess file
```
AuthType Basic
AuthName "Authorized Users Only"
AuthUsersFile /etc/httpd/authpass
Require vaild-user apache

```
Then restart the apache service
```
systemctl restart apache2
```



