# How to Repair MySQL Database in Linux?

# For Ubuntu and Debian, enter:

    service mysql stop

# To back up your database file, type:

    cp -r /var/lib/mysql /var/lib/mysql_backup

#  Restart the MySQL server by running the following command in your Linux system:

    service mysqld start

#  As the root user, enter the below command

    cd /var/lib/mysql

#  Check the database and all its tables for corruption by typing the command:

    mysqlcheck database_name

#  To check a specific database table for errors, type the command:

    mysqlcheck database_name table_name

#   If the table is not corrupted, an OK message is displayed. However, if the database table displays any errors, you need to repair it by using the following command:

    mysqlcheck –r database_name table_name

#   If running the mysqlcheck command does not fix the issue, proceed to the next step.


#   Stop your server using any of the below commands for your Linux distribution:

#   For Debian and Ubuntu, use:

    service mysql stop

#   Type the following:

    cd /var/lib/mysql

#   Check corrupt tables in the database, by using the following command:

    myisamchk table_name

#   To check all of the database tables, type the following command:

    myisamchk *.MYI

#   Once you have identified the corrupted tables in the database, use the mysqlchk command to repair the tables by following this command:

    myisamchk –recover table

#   For Debian and Ubuntu, type:

    service mysql start

#   Open MySQL configuration file “my.cnf”. The location of the my.cnf file on Debian and Ubuntu, the configuration file is located in the ‘/etc/mysql’ directory. Once you’ve located my.cnf file, find the [mysqld] section. In the [mysqld] section, add the following line:

    innodb_force_recovery=4

#   innodb_force_recovery=4

    service mysql restart

#   Run the below command to export all of the databases to the databasesbkp.sql file:

    mysqldump -u root -p –all-databases > databasesbkp.sql

#   Stop MySQL Server

    service mysql restart

    cd /var/lib/mysql

    rm -rf database

#   Open my.cnf file again, and comment out the following line:

    #innodb_force_recovery=4  

#   Star MySQL Server

    service mysql restart

#   restoring the database from the backup

    mysql -u root -p < databasesbkp.sql