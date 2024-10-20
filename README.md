# test_db

A sample database with an integrated test suite, used to test your applications and database servers.

This repository was migrated from [Launchpad](https://launchpad.net/test-db).

See usage in the [MySQL docs](https://dev.mysql.com/doc/employee/en/index.html).

## CS 5200 Version  

This version is prepared for **CS 5200 (Database Management Systems)** by **Ildar Akhmetov**. The setup includes instructions for deploying the database using Docker, aligning with the Docker environment used in the course.

## Where it comes from  

The original data was created by **Fusheng Wang** and **Carlo Zaniolo** at Siemens Corporate Research. The data is in XML format:  
[http://timecenter.cs.aau.dk/software.htm](http://timecenter.cs.aau.dk/software.htm).  

**Giuseppe Maxia** designed the relational schema, and **Patrick Crews** exported the data in relational format.  

The database contains around **300,000 employee records** and **2.8 million salary entries**, resulting in a 167 MB export file. The data, though generated, includes inconsistencies that are left intentionally for educational data cleaning exercises.

## Prerequisites  

You need a **MySQL database server (5.0+)**. The instructions below assume you have MySQL installed and running, following the CS 5200 Docker instructions.

Ensure the MySQL user executing the commands has the following privileges:

---

## Database Import Instructions

0. **Run the Container**  

If you haven't already, start your local MySQL container:

1. **Clone the Repository**  

```bash
gh repo clone cs5200-vankhoury/test_db
cd test_db
```

2. **Copy the SQL Files to the Container**  

If you are in the directory containing the SQL dumps:

```bash
docker cp . mysql-container:/tmp/
```

This command copies the SQL files to the `/tmp/` directory inside the MySQL container.

3. **Log in to the Container**  

Run the following command to log in to the container with bash:

```bash
docker exec -it mysql-container bash
```

4. **Execute the Main SQL Dump**

Inside the container, navigate to the `/tmp` directory and import the primary database dump:

```bash
cd /tmp
mysql -t -u root -p < employees.sql
```

Enter the MySQL root password when prompted.

Import should take some time from a few seconds to a few minutes, depending on your system.

You should expect to see the output similar to the following (where the time may vary):

```
INFO
CREATING DATABASE STRUCTURE
INFO
storage engine: InnoDB
INFO
LOADING departments
INFO
LOADING employees
INFO
LOADING dept_emp
INFO
LOADING dept_manager
INFO
LOADING titles
INFO
LOADING salaries
data_load_time_diff
00:00:18
```

---

## Testing the Installation  

After installing, you can verify the setup by running one of the test scripts inside the container.

```bash
mysql -t -u root -p < test_employees_sha.sql
```

Alternatively:

```bash
mysql -t -u root -p < test_employees_md5.sql
```

If successful, you should see the following output:

```
+----------------------+  
| INFO                 |  
+----------------------+  
| TESTING INSTALLATION |  
+----------------------+  
```

And a matching table summary with **OK** status for all tables:

```
+--------------+---------------+-----------+
| table_name   | records_match | crc_match |
+--------------+---------------+-----------+
| employees    | OK            | ok        |
| departments  | OK            | ok        |
| dept_manager | OK            | ok        |
| dept_emp     | OK            | ok        |
| titles       | OK            | ok        |
| salaries     | OK            | ok        |
+--------------+---------------+-----------+
```

---

## Original Project Credits  

This database and dataset were created by **Fusheng Wang** and **Carlo Zaniolo**. The relational schema was built by **Giuseppe Maxia**, and the data was exported to relational format by **Patrick Crews**.  

The original project was hosted at [Launchpad](https://launchpad.net/test-db), with further documentation available in the [MySQL Employee Sample Database](https://dev.mysql.com/doc/employee/en/index.html).  

---

## DISCLAIMER  

To the best of our knowledge, this data is **fabricated** and does not represent real individuals. Any similarities to actual persons are purely coincidental.

---

## LICENSE  

This work is licensed under the [Creative Commons Attribution-Share Alike 3.0 Unported License](http://creativecommons.org/licenses/by-sa/3.0/).  

---

This version is tailored for use in **CS 5200 at Northeastern University**. Please follow the Docker-specific instructions above for installation and testing within the course framework.