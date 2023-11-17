#"oldstable" debian version
FROM debian:bullseye

# -q for quiet
RUN apt-get update -yq \
&& apt-get upgrade -y \
&& apt-get install mariadb-server -y \
&& apt-get clean -y 

#copy our own configuration file into the container folder
COPY conf/my_conf.cnf /etc/mysql/mariadb.conf.d/50-server.cnf

# mariadb setup, here or in a separate script. more info in mariadb_start.sh file
RUN service mariadb start \
&& sleep 5 \
&& mariadb -u root -p"${MARIA_ROOT_PWD}" -e "CREATE DATABASE IF NOT EXISTS \`${MYSQL_DB}\`;" \
&& mariadb -u root -p"${MARIA_ROOT_PWD}" -e "CREATE USER IF NOT EXISTS \`${MYSQL_USER}\`@'localhost' IDENTIFIED BY '${MYSQL_PWD}';" \
&& mariadb -u root -p"${MARIA_ROOT_PWD}" -e "GRANT ALL PRIVILEGES ON \`${MYSQL_DB}\`.* TO \`${MYSQL_USER}\`@'%' IDENTIFIED BY '${MYSQL_PWD}';" \
&& mariadb -u root -p"${MARIA_ROOT_PWD}" -e "ALTER USER 'root'@'localhost' IDENTIFIED BY '${MARIA_ROOT_PWD}';" \
&& mariadb -u root -p"${MARIA_ROOT_PWD}" -e "FLUSH PRIVILEGES;" \
&& mariadb-admin -u root -p"${MARIA_ROOT_PWD}" shutdown

CMD ["mysqld_safe"]

