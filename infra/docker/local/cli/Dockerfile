FROM amazonlinux:2

# Generics
RUN amazon-linux-extras enable php7.4 ; yum clean metadata ; yum install -y curl git unzip

# PHP
RUN yum install -y php php-cli php-common php-json php-xml php-memcached php-curl php-mbstring php-bcmath php-gmp php-intl php-opcache php-gd php-zip php-sqlite3 php-pdo php-mysqlnd php-sodium php-redis
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer
RUN composer self-update --1

# PHP Configs
ADD etc/php.d/ /etc/php.d/

# JWT Certificates
ADD etc/jwt/private.pem /etc/jwt/private.pem
ADD etc/jwt/public.pem /etc/jwt/public.pem

# Code Sniffer
RUN curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar
RUN mv phpcs.phar /usr/bin/phpcs
RUN chmod +x /usr/bin/phpcs

# Code Sniffer - Fixer
RUN curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcbf.phar
RUN mv phpcbf.phar /usr/bin/phpcbf
RUN chmod +x /usr/bin/phpcbf

WORKDIR /home/app

CMD tail -f
