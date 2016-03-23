title: linux install jdk
date: 2015-10-13 10:13:10
tags:
- linux
- java

---
install jdk
<!--more--> 
## download
[download jdk](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
chose  Linux x64	172.84 MB  	jdk-8u60-linux-x64.tar.gz

## delete default jdk


## extract 
~~~bash
tar -zxvf jdk-8u60-linux-x64.tar.gz
~~~

## move to /user/lib/java
~~~bash
mv ./jdk1.8.0_60 /usr/lib/java/jdk1.8.0_60
~~~

## config
~~~bash
vi /etc/profile
~~~
    # java config
    export JAVA_HOME=/usr/lib/java/jdk1.8.0_60
    export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
    export PATH=$PATH:$JAVA_HOME/bin
  
## excute
~~~bash
source /etc/profile
~~~

## validate
~~~bash
java -version
~~~

create a java file

~~~bash
vi Hello.java
~~~

~~~java
public class Hello{
  public static void main(String args[]){
    System.out.println(" Hello Linux, I'm Java!");
  }
}
~~~

compile excute
~~~bash
javac Hello.java
java Hello
~~~

bingo
