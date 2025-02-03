# Pull offcial docker image from docker hub
FROM mysql:oraclelinux9 

# Labels 
LABEL OS="Oracle Linux 9"
LABEL Maintainer="Mahesh Gupta"
LABEL Email="mahesh.gupta1804@gmail.com"

# Exporting the environment variable #
ENV MY_SQL_ROOT_PASSWORD="root123"
ENV MY_SQL_DATABASE="mydb"
ENV MY_SQL_USER="admin"
ENV MY_SQL_PASSWORD="admin123"

# Expose the port
EXPOSE 3306

# Command to run mysql server
CMD [ "mysqld" ]
