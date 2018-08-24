# Spring PetClinic Sample Application

*Note: This project was forked from [spring-projects/spring-petclinic](http://github.com/spring-projects/spring-petclinic) to be used as a sample application for various Knowledge sessions.*

## Understanding the Spring Petclinic application with a few diagrams
<a href="https://speakerdeck.com/michaelisvy/spring-petclinic-sample-application">See the presentation here</a>

## Running petclinic locally

Clone the repo:

```
	git clone https://github.com/savishy/spring-petclinic
	cd spring-petclinic
```

This project packages a restributable Maven Wrapper. Maven installation is not required to run this project.

You can use the built-in Maven Wrapper to run Petclinic:

:exclamation: Note, Java Development Kit must be present and JAVA_HOME environment variable must be set.

On Linux
```
	./mvnw spring-boot:run
```

On Windows:
```
mvnw.cmd spring-boot:run
```

If you have an install of Maven, you can also run using Maven as `mvn | mvn.cmd spring-boot:run`


You can then access petclinic here: http://localhost:8080/

## Building Petclinic (JAR)

`./mvnw install` on Linux systems. `mvnw.cmd install` on Windows.

## Changing the default port

The application runs on port 8080 by default. You can change the port via a Spring Boot command-line argument.


## Database configuration

* In its default configuration, Petclinic uses an in-memory database (HSQLDB) which gets populated at startup with data.
* A similar setup is provided for MySql in case a persistent database configuration is needed.

### Start a MySQL Server

You could start a MySql database with docker:

```
docker run -e MYSQL_ROOT_PASSWORD=petclinic -e MYSQL_DATABASE=petclinic -p 3306:3306 mysql:5.7.8
```

### Modify `pom.xml`

Make sure the `mysql-connector-java` artifact in [pom.xml](pom.xml) is uncommented:

```
        <dependency>
             <groupId>mysql</groupId>
             <artifactId>mysql-connector-java</artifactId>
             <version>${mysql-driver.version}</version>
        </dependency>
```

### Modify `data-access.properties`

Edit the file [src/main/resources/spring/data-access.properties](src/main/resources/spring/data-access.properties).

Make sure it has the following values:

* Note: here its assumed the DB is at 127.0.0.1 with port 3306.
* Note: It's assumed the DB user is root with password `petclinic`.

```
jdbc.initLocation=classpath:db/mysql/initDB.sql
jdbc.dataLocation=classpath:db/mysql/populateDB.sql

jpa.showSql=true

jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://127.0.0.1:3306/petclinic?useUnicode=true&characterEncoding=UTF-8
jdbc.username=root
jdbc.password=petclinic

# Property that determines which database to use with an AbstractJpaVendorAdapter
jpa.database=MYSQL
```

Make sure to compile and run the application.
