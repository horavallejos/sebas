FROM amazonlinux:2

# Generics
RUN amazon-linux-extras enable php7.4 ; yum clean metadata ; yum install -y curl git unzip

# PHP
RUN yum install -y php php-cli php-common php-json php-xml php-memcached php-curl php-mbstring php-bcmath php-gmp php-intl php-opcache php-gd php-zip php-sqlite3 php-pdo php-mysqlnd php-sodium php-redis
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer
RUN composer self-update --1

# PHP Configs
ADD etc/php.d/ /etc/php.d/

# Apache
RUN yum install -y httpd mod_ssl
RUN rm -f /etc/httpd/conf.d/*

# Apache Configs
ADD etc/httpd/conf.d/ /etc/httpd/conf.d/
ADD etc/httpd/conf/ /etc/httpd/conf/
RUN rm /etc/httpd/conf.modules.d/00-dav.conf
RUN rm /etc/httpd/conf.modules.d/00-lua.conf
RUN rm /etc/httpd/conf.modules.d/01-cgi.conf
RUN rm /etc/httpd/conf.modules.d/10-proxy_h2.conf

# Certificate
ADD etc/httpd/certs/ /etc/httpd/certs/

# JWT Certificates
ADD etc/jwt/private.pem /etc/jwt/private.pem
ADD etc/jwt/public.pem /etc/jwt/public.pem

EXPOSE 80
EXPOSE 443

# Service
CMD httpd -D FOREGROUND
