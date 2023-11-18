# https://docs.docker.com/engine/reference/builder/
FROM debian:bullseye

# installation of php, php-fpm (fastCGI Manager) and php-mysql
RUN apt-get update -yq \
&& apt-get upgrade -y \
&& apt-get install -y wget \
&& apt-get install -y php7.3 php-fpm php-mysql mariadb-client \
&& wget https://fr.wordpress.org/wordpress-6.2.2-fr_FR.tar.gz -P /var/www \
# -x to extract -z to use gzip -f to choose the archive file
&& cd /var/www && tar -xzf wordpress-6.2.2-fr_FR.tar.gz && rm wordpress-6.2.2-fr_FR.tar.gz \
&& chown -R root:root /var/www/wordpress
