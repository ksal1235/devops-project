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
