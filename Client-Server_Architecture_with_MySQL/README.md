# Client-Server Architecture with MySQL

#### Client-Server architecture is a network design where client devices (such as computers, smartphones, or tablets) request services or resources from a server. The server, which is typically a powerful computer or system, processes the requests and provides the requested resources or services back to the clients. This architecture is a fundamental concept in networking and web application development.

#### A simple diagram of Web Client-Server architecture is presented below.

  ![image](https://github.com/user-attachments/assets/c894e5bc-a98d-48a1-a8df-6a1e76dc2942)

In the example above, a machine that is trying to access a Web site using Web browser  is a client and it sends HTTP requests to a Web server (Apache, Nginx, IIS or any other) over the Internet.

- If we extend this concept further and add a Database Server to our architecture, we can get this picture:

![image](https://github.com/user-attachments/assets/f66395a6-ccf0-4728-84b2-1732a53a3e30)

- In this case, our Web Server has a role of a "Client" that connects and reads/writes to/from a Database (DB) Server (MySQL, MongoDB, Oracle, SQL Server or any other), and the communication between them happens over a Local Network (it can also be Internet connection, but it is a common practice to place Web Server and DB Server close to each other in local network).
- The setup on the diagram above is a typical generic Web Stack architecture that you have already implemented in previous projects (LAMP, LEMP, MEAN, MERN), this architecture can be implemented with many other technologies - various Web and DB servers, from small Single-page applications SPA to large and complex portals.

- Today, we will be implementing a server-client architecture using MYSQL database managemet system on aws EC2 instance.
## Steps involved:
1. Provisioning a New Two EC2 instance of t2.micro family with Ubuntu Server 24.04 LTS (HVM):
```
Server A name - `mysql server`
Server B name - `mysql server`
```
![image](https://github.com/user-attachments/assets/7a28f06e-d49f-443d-b249-6c196c2f6107)

2. Connect to your instance via ssh

```
  ssh -i <key-pair-name> ubuntu@<ip-address>
```
![image](https://github.com/user-attachments/assets/d97512bb-a7d7-47c7-9255-2487ed1117a6)

3. Update and Upgrading packages in both instances:

```
sudo apt update && sudo apt upgrade -y
```
![image](https://github.com/user-attachments/assets/265f99f8-b544-47d1-a800-f854db45c4f0)

4. On mysql server Linux Server install MySQL Server software.

```
sudo apt install mysql-server
```
![image](https://github.com/user-attachments/assets/e81375ec-5e84-4104-ac27-fb9c825e2fec)

5. Edit the mysql configuration file to allow remote connections.

```
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
![image](https://github.com/user-attachments/assets/33443438-e26b-43f7-bb60-cc29ed2f927b)

6. Find the line that begins with bind-address and change it to 0.0.0.0

```
    bind-address = 0.0.0.0
```
![image](https://github.com/user-attachments/assets/afb7da86-82b2-4527-ac68-5d49ab5d34b4)

save and close file.
7. Create a user that can connect remotely and grant all privileges.
Setting Up the password
```
sudo mysql 
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Golu123!@#';
exit
```
As we did before Also.

Now Creating User and Assigning the Privileges to it.
```
CREATE USER 'shoeb'@'%' IDENTIFIED BY 'Golu123!@#';
GRANT ALL PRIVILEGES ON *.* TO 'shoeb'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
![image](https://github.com/user-attachments/assets/2bd875bb-fc46-4e1f-8585-f2ea54f93eac)

8. On the client instance, install mysql - client
```
sudo apt install mysql-client
mysql --version
```

# Note: it is important to know that mysql server uses port 3306 bydefault, so it is essential to allow our mysql client be able to connect to the mysql server, in order to do this, we should edit the inbound rules of the security group of server instance, to do this, follow the steps below:

- Creating the New Security Group. We have Option to create On same EC2 Page.
![image](https://github.com/user-attachments/assets/7106b98d-8b73-4b6d-9399-1793ac130bb2)

- Add new inbound rules by adding a custom tcp , set to port 3306 and allow the ip address from client instanvce (use private IP) example: ip-address/32
![image](https://github.com/user-attachments/assets/a1991a3d-18ba-4967-9773-fb919514707f)
- save it
  
- Click on Mysql server instance and Click on action then go To Security and Add Security Group which we created.
![image](https://github.com/user-attachments/assets/8d8e88df-bc1c-488e-a59b-bc0105fd77a5)

# Connecting to Mysql server from the mysql client.

```
mysql -u username -p -h server-ipaddress
```
![image](https://github.com/user-attachments/assets/dfe4ee67-d5ec-4e70-ac96-4caf8605cf3b)
We can also Connect Using Private Ip Because both server rely on Same Netwrok.

- We can use the show database command to verify you are properly connected and logged in.

```
 SHOW DATABASES;
```
![image](https://github.com/user-attachments/assets/c38eeb17-5344-43d6-8fda-e924a6bc363b)

# Manipulating the database.
- Create database.
```
   CREATE DATABASE Demodatabase;
```
- Select the database to use it.
```
 USE Demodatabase;
```
- Create tables.
```
  CREATE TABLE shoeb (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL
    );
```
- Insert data in to the tables.
```
INSERT INTO shoeb (name, email) VALUES ('khan shoeb', 'shoeb@gmail.com');
```
- Verify inserted data
```
 SELECT * FROM shoeb;
```
![image](https://github.com/user-attachments/assets/6d0bf89e-8002-44b8-ad3b-e736f3dfe772)

- Drop the table.

```
 DROP TABLE shoeb;
```
Deleting the Table.

- Drop the Database.

```
 DROP DATABASE Demodatabase;
```
Deleting the Database.

# Conclusion.











