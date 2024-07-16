# This Dockerfile derives the image from the base slotix/dbs-mysql image
# with necessary permissions and custom config to enable mysql replication.
FROM mysql:8.3.0

# copy sql script to create database and table structures.
COPY mysql.cnf /etc/mysql/conf.d/
COPY ./docker-entrypoint-initdb.d /docker-entrypoint-initdb.d
ADD products.csv /var/lib/mysql-files