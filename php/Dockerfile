FROM nanoninja/php-fpm:7.1.14

LABEL maintainer="phanvuhoang@gmail.com"
LABEL php_version="7.1.14"
ENV INSTALL_DIR /var/www/html

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
	&& chmod +x wp-cli.phar

RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
    git vim

RUN groupadd -g 1000 app \
 && useradd -g 1000 -u 1000 -d /var/www -s /bin/bash app

RUN chown -R www-data:app /var/www/html &&\
    chmod g+w /var/www/html -R



RUN \
  chmod 777    /var/www/ &&\
    chmod 777 /var/www/html

USER www-data
RUN git clone https://github.com/arialdomartini/oh-my-git.git ~/.oh-my-git && echo source ~/.oh-my-git/prompt.sh >> ~/.bashrc

# install wp-cli
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar &&\
    chmod +x wp-cli.phar &&\

USER root
RUN mv wp-cli.phar /usr/local/bin/wp
USER www-data

WORKDIR $INSTALL_DIR