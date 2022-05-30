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

<img src="/screenshot/connector.png" width="600"/>

```
maxPostSize= "209715200"
URIEncoding="UTF-8"
relaxedQueryChars="[,]"
```  

Multipart config. [open terminal and run]
<img src="/screenshot/multipart.png" width="600"/>

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
Optimize Tomcat: Run the command
```
sudo nano /etc/default/tomcat9
``` 
Then uncomment and add Java_home path [N:B-> make sure you copy your path, dont paste] check the video liked below.

<img src="/screenshot/javahome.png" width="600"/>

```
JAVA_HOME=/usr/lib/jvm/java-8-openjdk  
``` 
Still on the same file, add this below Java_opts 
NB:Your machine should be 8G RAM , otherwise customize to fit your RAM size.
```
JAVA_OPTS="${JAVA_OPTS} -Xmx2048m -Xms1024m -XX:PermSize=512m -XX:MaxPermSize=512m -XX:NewSize=256m"

``` 

Create OpenMRS directory and and grant user permision to tomcat9
```
sudo mkdir /var/lib/OpenMRS 
sudo chown -R tomcat:tomcat /var/lib/OpenMRS/
sudo chmod -R 755 /var/lib/OpenMRS*
``` 
Redirect logs to catalina : Run the command
```
/lib/systemd/system/tomcat9.service
``` 
Then comment out the line:

<sub>*SyslogIdentifier=tomcat9*</sub>

Once done, in the same file, add this 2 lines: just below the line commented out
```
StandardOutput=append:/var/log/tomcat9/catalina.out
StandardError=append:/var/log/tomcat9/catalina.out
``` 
Under *Service* still in same file, add this below it
```
ReadWritePaths=/var/lib/OpenMRS/
``` 
Then save the chanes [ press ctrl + O, press ENTER, then ctrl + X]


###### Tomcat 9 Rewrite:

Create service.d file by running the command:
```
sudo mkdir /etc/systemd/system/tomcat9.service.d
```

Create blank file in the directory and name it logging-allow.conf, run:
```
sudo nano logging-allow.conf
```
Once created, add this: and save changes as specified ealier.
```
ReadWritePaths=/var/lib/OpenMRS
```

Reload the daemon process and restart tomcat9:
```
sudo systemctl daemon-reload
sudo systemctl restart tomcat9
```

Additional: FYI [ commands to start,stop anf restart tomcat9]

```
sudo service tomcat9 start
sudo service tomcat9 stop
sudo service tomcat9 restart
sudo service tomcat9 status
```

### Install mysql 5.6 ubuntu 20

if you have existing different version, uninstall the proceed as stated:

In your terminal run:
```
sudo add-apt-repository 'deb http://archive.ubuntu.com/ubuntu trusty universe'
````

Then run this 
```
sudo add-apt-repository 'deb http://kr.archive.ubuntu.com/ubuntu xenial main'
```
Update,and install:
```
sudo apt update
```

```
sudo apt-get install mysql-server-5.6
```

Change ownership and set defaults then restart
```
sudo touch /var/run/mysqld/mysql.sock
```

```
sudo chown mysql:mysql /var/run/mysqld
```
```
sudo update-rc.d mysql defaults
```
```
sudo service mysql restart
```

Commands to start,stop ,restart and check status Mysql
```
sudo service mysql start
sudo service mysql stop
sudo service mysql restart
sudo service mysql status
```

### Reference

- [Youtube Installation guide tutorial Timz owen [mysql5.6] ](https://youtu.be/kTtxQdYoluo)


<img src="/screenshot/mysql.png" width="300"/> <img src="/screenshot/tomcat.png" width="300"/>
  
-  [Youtube Installation guide tutorial Timz owen [Tomcat / Java] ](https://youtu.be/nf8h4Y5a9C0)

 *<sub>cc: borrowed from HealthIT & Palladium developers Original guide.*</sub>

