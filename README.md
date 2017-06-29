# Performance Improvement of OpenEdX using RocksDB

#### RocksDB:
 * RocksDB is a C++ library providing an embedded key-value store, where keys and values are arbitrary byte streams. It was developed at Facebook based on LevelDB and provides backwards-compatible support for LevelDB APIs.
 * RocksDB is optimized for Flash with extremely low latencies. RocksDB uses a Log Structured Database Engine for storage,which is written entirely in C++.
 * RocksDB features highly flexible configuration settings that may be tuned to run on a variety of production environments, including pure memory, Flash, hard disks or HDFS. It supports various compression algorithms and good tools for production support and debugging.
 - - -
 
* [Installation](https://github.com/fresearchgroup/performance-improvement-of-openedx#installation)
* [Technologies and Languages Used](https://github.com/fresearchgroup/performance-improvement-of-openedx#technologies-and-languages-used)
* [Usage](https://github.com/fresearchgroup/performance-improvement-of-openedx#usage)
* [Contributing](https://github.com/fresearchgroup/performance-improvement-of-openedx#contributing)
* [Credits](https://github.com/fresearchgroup/performance-improvement-of-openedx#credits)
* [License](https://github.com/fresearchgroup/performance-improvement-of-openedx#license)

- - -
#### Installation:
This document provides shall provide a step-by-step guide to install the following softwares:

* OpenEdx Devstack:

* MariaDB 10.2: Here are the commands to install MariaDB on your Ubuntu system:
     ```
     1. sudo apt-get install software-properties- common
     ```
     ```
     2. sudo apt-key adv -- recv-keys -- keyserver hkp://keyserver.ubuntu.com:800xF1656F24C74CD1D8 3.sudo add-apt- repository &#39;deb [arch=amd64,i386,ppc64el]http://mirrors.neusoft.edu.cn/mariadb/repo/10.2/ubuntu xenial main
     ```
     ```
     3. sudo apt update
     ```
     ```
     4. sudo apt install mariadb-server
     ```
     
     After insatlling MariaDB,you need to add the following lines to the bottom of your sources.list file(/etc/apt/sources.list)
     ```
     deb[arch=amd64,i386]http://mirrors.neusoft.edu.cn/mariadb/repo/10.2/ubuntu
     ```
     ```
     xenial main deb-src http://mirrors.neusoft.edu.cn/mariadb/repo/10.2/ubuntu xenial main
     ```
     (You can create a backup of your sources.list file for safety purpose)
     
  * Steps to install RocksDB plugin:
     ```
     sudo apt install mariadb-plugin-rocksdb
     ```
     The only configuration needed to enable the plugin is add the following command in the [server],[mysqld] or [mariadb]    
     section of my.cnf file present in etc/mysql.
     ```
     plugin-load- add=ha_rocksdb.so
     ```
     And the restart MariaDB.
   
 * Apache-jmeter-3.2:
     
     1.Download the Binaries distribution in tgz archive from-
     http://jmeter.apache.org/download_jmeter.cgi?Preferred=http%3A%2F%2Fwww-eu.apache.org%2Fdist%2Feu.apache.org%2Fdist%2F
  
     2.Instead of installing various plugins manually. Install Plugins Manager once and it will do it all for you:installing,up
     grading and uninstalling.
  
     Download the Plugins Manager JAR file from https://jmeter-plugins.org/downloads/all/ and extract it into JMeter's lib/ext
     directory.
     
     3.MySQL provides connectivity for client applications developed in the Java programming language with MySQL Connector/J,
     a driver that implements the Java Database Connectivity (JDBC) API. MySQL Connector/J is distributed as a .zip .tar.gz
     archive,available for download from https://dev.mysql.com/downloads/connector/j/3.1.html.

     Install the Connector/J package using the binary distribution. The binary distribution provides the easiest method for 
     installation.
     
     * Select version as 5.0.8
     * Select operating system as platform independent.
     * Download the .zip archive and extract it in apache-jmeter- 3.2/bin/lib directory.
     
     4.`Creating a Test Plan for Database Testing`:
     
     * Add thread group.
     * Add JDBC Connection Configuration and provide the details of the database.
       Database URL: jdbc:mysql://hostname:port_number/database
       JDBC Driver Class: com.mysql.jdbc.Driver
     * Add JDBC Request.
     * Add Listeners either in the form of tree,graph or table.
     * Run and validate.
     
     5.`Creating assertions for JDBC Test Plan` :
     
     * Add a response assertion.
     * Add variable name in JDBC Request.These are basically columns that correspond to the result.You can name it as for say
     if you have 4 columns then A,B,C,D.
     If you want assertion for only A and C then add A,,C.
     * Set response field to text as Text Response and add Pattern to Test.
     * Add Listeners-&gt; Assertion Results.
     * Run and validate.
     
     6.`How to read data from CSV file(Parameterization)` :
     
     * Add Config Element-&gt;CSV Data Set Config.
     * Add filename as xyz.csv if you are on bin folder,otherwise provide the path of the file.
     * Update value fields : Remove the variable names in the JDBC Request to ${variable_name},where variable_name is the name
     of the variable in the CSV file.
     * No need to give variable names as we have already given it in CSV file.
     * Delimiter=,
     * Rest as default.Run and validate.
     
     7.`How to add Timers in jmeter` :
     
     * Add a Simple Controller- to do all your samples in a logical way.
     * Add timers.We generally use Constant Timers and Uniform Random Timer.
     * Constant Timer : You can add thread delay here which is in milliseconds.
     * In case if you add more than 1 requests having individual timers,then for request 1 time delay will be timer 1+ timer 2
     and so on.For request 2 you will be having time delay of timer 2+timer 3 and so on.
     * Uniform Random Timer: Here we have 2 fields:
     -Random Delay Max
     -Constant Delay Offset

     Random Delay=0.X*Random Delay Max + Constant Delay Offset
     X: any value from [0,9]
 ---    
     
     
#### Technologies and Languages Used:
    
 | Technologies      | Languages | Storage Engines | 
 |-------------------|:---------:|:---------------:|
 | Ubuntu 16.04 |    | MySQL     | InnoDB          |
 | OpenEdx |         | MariaDB   | RocksDB         |    
 | Apache-Jmeter-3.2 | 
 | Spawner |
 
 ---

   

   



#Synopsis of the Project 

EdX is a MOOC(Massive Open Online Course) platform started by MIT and Harvard in collaboration for
revolutionizing online education. EdX is among the most popular MOOC’s in the world because of the
advance features it provides for making online education of student fruitful and more effective worldwide. It
also provides the author an effective way to design a course.
OpenEdX is the open source platform based on the EdX platform and is created on the Django framework
(written in python). RocksDB, a storage engine has been presented by Facebook Inc. as a better alternative to
InnoDB, both in terms of throughput and reduced storage space requirements.
The project deals with integration of MongoRocks and MyRocks, built by integrating RocksDB into
MongoDB and MySQL, respectively, in the OpenEdX framework and run benchmark tests to check for its
feasibility and viability.

#Product Scope

The OpenEdX system or platform provides an easy and effective way to build MOOC’s for students and
others to opt for free online courses. The benefits of this is that the traditional learning methods (like
classrooms with black boards) are upgraded with online interactive support using computers as a tool to
provide all kind of courses in interactive manner.
It also provides an interactive platform for the author to make/design a high quality online course with
different kinds of grading systems and other facilities.
Minimizing space amplification is important to efficient hardware use because storage space is the bottleneck
in production environments. SSDs process far fewer reads/s and writes/s during peak times under InnoDB
than what the hardware is capable of. The throughput level under InnoDB is low, not because of any
bottleneck on the SSD or the processing node — e.g., CPU utilization remains below 40% — but because the
query rate per node is low. RocksDB provides an efficient solution to this issue, under production conditions.
As a result it may be possible to use the same engine enabled database system for the OpenEdX framework,
thus enabling more efficient usage of disk space and faster execution time.
