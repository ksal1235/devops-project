## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

### STEP1 Provisioning a new EC2 instance of t2.micro family with Ubuntu Server 24.04 LTS (HVM):

![image](https://github.com/user-attachments/assets/9e0fce11-72a4-4e51-b0fe-5fd198b00b52)


### Step2 — Installing Apache and Updating the Firewall:
__a.__ Updating the machine:
```
sudo apt update
```

![image](https://github.com/user-attachments/assets/c78a22e9-de0f-408e-b89f-2f88332738b6)

__b.__	Installing apache web-server:
```
sudo apt install apache2 
```
![image](https://github.com/user-attachments/assets/2e0dbc66-9bd0-48e5-b5f2-3afd1db0bcdc)

__c.__ Checking the status of apache web-server:
```
sudo systemctl status apache2
```
![image](https://github.com/user-attachments/assets/dcc30c58-4207-4b4b-b0fb-7490c0012622)

__d.__ Accessing on Browser
```
http://13.201.34.243:80
```
![image](https://github.com/user-attachments/assets/81e46beb-7e4c-4ca8-b89f-91028fc6b029)

### STEP3 Installing MySQL
__a.__ Installing the mysql:
```
sudo apt install mysql-server
```
![image](https://github.com/user-attachments/assets/b4b1a0aa-fd87-4df5-8366-b6825ef348ca)

__b.__ Setting up the password :
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Golu123!@#';
```
![image](https://github.com/user-attachments/assets/eee7970e-331e-4921-8f10-60f71efc4a8d)

### Step4 Installing PHP to display dynamic content to the end user:

__a.__ Installing the php:

```
sudo apt install php libapache2-mod-php php-mysql
```
![image](https://github.com/user-attachments/assets/41e18627-de1b-475b-82bd-f758d86b1ee2)

__b.__ Checking the version of php:

![image](https://github.com/user-attachments/assets/d19bba68-1e52-4b38-a8b3-51d6d7a6fe20)

### Step 5 — Creating a Virtual Host for your Website using Apache:

__a.__	Create the directory for projectlamp using 'mkdir':
```
sudo mkdir /var/www/projectlamp
```
![image](https://github.com/user-attachments/assets/63d9a4ae-1d0d-437a-8927-f3f7a4a8255a)

__b.__	Changing Ownership
```
sudo chown -R $USER:$USER /var/www/projectlamp
```
![image](https://github.com/user-attachments/assets/6eb09ecb-d5be-49a3-97c6-10f3b40e1d26)

__c.__		Creating the Configuration file
```
sudo vi /etc/apache2/sites-available/projectlamp.conf
```
![image](https://github.com/user-attachments/assets/673098c2-edfa-47d5-a7f2-23fc3e4d547e)


__d.__		Enable the new virtual host
```
sudo a2ensite projectlamp
```
![image](https://github.com/user-attachments/assets/0a4c79e6-1dc4-41b6-bef6-296ff650ffa6)


__e.__		Disable apache default website

```
sudo a2dissite 000-default
```

![image](https://github.com/user-attachments/assets/8dd992c2-1405-4093-8b02-31db7a5622b6)

__f.__ To check the  syntax error
```
sudo apache2ctl configtest
```

![image](https://github.com/user-attachments/assets/04e2ea06-7973-42cb-bc1d-bca6b204ce2f)

__e.__  reloading the apache web-server
```
sudo systemctl reload apache2
```
![image](https://github.com/user-attachments/assets/3b00aa4a-33d8-47bd-8c90-b453ec24d4b0)


__f.__  Accessing the web-server on browser

```
http://13.201.34.243/
```
![image](https://github.com/user-attachments/assets/054f346b-2156-4963-b09a-ace40f139c98)

### Step 6 — Enable PHP on the website.

__a.__  Editing /etc/apache2/mods-enabled/dir.conf to change the behaviour.

```
sudo vi /etc/apache2/mods-enabled/dir.conf
```
![image](https://github.com/user-attachments/assets/2948be88-edb8-4fd7-8693-b76d03a2b93b)



![image](https://github.com/user-attachments/assets/0765480c-5806-479d-b8ea-c4dedd71f6a3)

__b.__	file named index.html will always take precedence over an index.php file. This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors.

```
vi /var/www/projectlamp/index.php
```
![image](https://github.com/user-attachments/assets/09b69dfd-729c-45d8-a475-37d15debeb92)

# Add the text below in the index.php file

```
vi /var/www/projectlamp/index.php
```
![image](https://github.com/user-attachments/assets/6f5924bc-f450-4312-9dec-02e67c6e130f)

![image](https://github.com/user-attachments/assets/a9db328c-4510-47ac-8af8-00482bbfd58a)


__c.__ Accessing the php page on browser.


```
http://13.201.34.243:80
```
![image](https://github.com/user-attachments/assets/a139385b-8f16-4adb-b51a-ef9964d8e663)



