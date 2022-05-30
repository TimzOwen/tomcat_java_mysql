# Installation guide for Tomcat9, mysql5.6 & Java 8 Ubuntu 20

#### installation commands for ubuntu 20 .


## Instalation commands for Java 

Run the following commands to install java jdk 8 .

```
sudo apt get update
```         

```
sudo apt install openjdk-8-jdk
```  

```
sudo apt-get update
```  

## Install tomcat9 ubuntu 20

We are going to remove existing tomcat version. ``` or install alongside as group```

Stop any tomcat running [```use right version```]
```
sudo service tomcat6 stop
```  

Remove any files from tomcat 6
```
sudo apt-get autoremove --purge tomcat6
```  

```
sudo apt-get update
```  

Now proceed to installing tomcat 9
```
sudo apt install tomcat9
```  

```
sudo apt install tomcat9-docs tomcat9-examples tomcat9-admin
```  

```
sudo apt-get update
```  
You are all done !!!!

You can check the status using ```sudo service tomcat9 status```


##### Configurations commands for Tomcat9 to run on OpenMRS & KenyaEMR
```
sudo nano /etc/tomcat9/server.xml

```  
Set the http connector to 200MB .[below connector]
```
maxPostSize= "209715200"
URIEncoding="UTF-8"
relaxedQueryChars="[,]"
```  

Multipart config. [open terminal and run]
```
sudo nano /usr/share/tomcat9-admin/manager/WEB-INF/web.xml
```  
Lines to edit are:
```
<max-file-size>209715200</max-file-size>
<max-request-size>209715200</max-request-size>

```  
cd to catalina.properties and edit:
```
sudo nano /var/lib/tomcat9/conf/catalina.properties
```  
at the end of the catalina.properties file add:
```
org.apache.tomcat.util.buf.UDecoder.ALLOW_ENCODED_SLASH=true
```  
Next, we add roles to tomcat users: run the command below
```
sudo nano /etc/tomcat9/tomcat9-users.xml
``` 
Then add the following lines, Rem to change the password to mactch your comp passwrd
```
<role rolename=”tomcat”/>
<role rolename=”manager-gui”/>
<role rolename=”admin-gui”/>
<user username=”admin” password=”PASSWORD” roles=” tomcat, manager-gui, admin-gui”/>
``` 
Optimize Tomcat
```
sudo apt-get update
``` 

```
sudo apt-get update
``` 

```
sudo apt-get update
``` 

```
sudo apt-get update
``` 


### Screenshots

<img src="art/1.png" width="200"/> <img src="art/2.png" width="200"/>

### Reference

- [Youtube Installation guide tutorial Timz owen [mysql5.6] ](https://youtu.be/kTtxQdYoluo)
  
-  [Youtube Installation guide tutorial Timz owen [Tomcat / Java] ](https://youtu.be/nf8h4Y5a9C0)

 *<sub><sub>cc: borrowed from HealthIT developers Original guide.*</sub></sub>

