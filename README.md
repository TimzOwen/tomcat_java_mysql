# Installation guide for Tomcat9, mysql5.6 & Java 8 Ubuntu 20

## installation commands for ubuntu 20 .


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


### Screenshots

<img src="art/1.png" width="200"/> <img src="art/2.png" width="200"/>

### Reference

- [Youtube Installation guide tutorial Timz owen [mysql5.6] ](https://youtu.be/kTtxQdYoluo)
  
-  [Youtube Installation guide tutorial Timz owen [Tomcat / Java] ](https://youtu.be/nf8h4Y5a9C0)



