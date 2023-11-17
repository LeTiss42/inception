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
&& mariadb -u root -p"rootpwd" -e "CREATE DATABASE IF NOT EXISTS \`ouidb\`;" \
&& mariadb -u root -p"rootpwd" -e "CREATE USER IF NOT EXISTS \`userdb\`@'localhost' IDENTIFIED BY 'mysqlpwd';" \
&& mariadb -u root -p"rootpwd" -e "GRANT ALL PRIVILEGES ON \`ouidb\`.* TO \`userdb\`@'%' IDENTIFIED BY 'mysqlpwd';" \
&& mariadb -u root -p"rootpwd" -e "ALTER USER 'root'@'localhost' IDENTIFIED BY 'rootpwd';" \
&& mariadb -u root -p"rootpwd" -e "FLUSH PRIVILEGES;" \
&& mariadb-admin -u root -p"rootpwd" shutdown \
&& echo "SUUUUUUUUUUUUUUUUUU"

CMD ["mysqld_safe"]

