# ListInstancesWithJDI

The simple project used for connecting to remote or local JVM using JDI (Java Debug Interface) 
and get all instances of a specified class. Currently tested on JDK 8

## Examples

To run an example firstly make sure you need to 

    1) get tools.jar (you can get it from C:\Program Files\Java\jdk1.8.0_231\lib) 
        from Oracle JDK Installation and put it to src\main\resources\scripts

    2) then you need to run install_to_maven (mvn should be in your PATH).

After that to test example run following commands:
set MAVEN_OPTS="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=56856"
mvn clean compile exec:java 

It compiles and executes java program. First, it set JDI address for socket listening.
After then program connects to itself (using address localhost:56856) gets VirtualMachine instance and uses it to get all instances of  java.lang.String class in current mvn JVM.

## IDE
Tested with NetBeans 11.0

## Source
The program connects to remote JVM using SocketConnector. After attaching to the JVM it gets the instance of JVM.
When getting an instance of a class you could get a com.sun.jdi.ObjectCollectedException exception. You can avoid it
by using vm.suspend(); and vm.resume() between getting instances of a class but it would freeze all remote JVM.
