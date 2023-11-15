#"oldstable" debian version
FROM debian:bullseye

# -q for quiet
RUN apt-get update -yq \
&& apt-get upgrade -y \
&& apt-get install mariadb-server -y \
&& apt-get clean -y 

#copy our own configuration file into the container folder
COPY conf/my_conf.cnf /etc/mysql/mariadb.conf.d/50-server.cnf
