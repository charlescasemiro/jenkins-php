FROM registry.redhat.io/ocp-tools-4/jenkins-agent-base-rhel8@sha256:5933efefc9d2e7dfbefec7c44b22cdd4fffc7bd62afd9517d2fca5bd84fb9970
USER root
RUN wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-linux.zip \
    && unzip -d /opt/ sonar-scanner-cli-4.8.0.2856-linux.zip \
    && wget -O phpunit https://phar.phpunit.de/phpunit-10.2.2.phar \
    && chmod +x phpunit \
    && mv phpunit /usr/local/bin/ \
    && dnf -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm \
                http://rpms.remirepo.net/enterprise/remi-release-8.rpm \
                glibc \
                nettle \
                dnf-plugins-core \
                dnf-utils \
                https://ftp.nluug.nl/pub/os/Linux/distr/pclinuxos/pclinuxos/apt/pclinuxos/64bit/RPMS.x86_64/lib64gcrypt11-1.5.6-2pclos2017.x86_64.rpm \
    && dnf module reset php -y\
    && dnf module install php:remi-8.1 -y \
    && yum install php81-php php81-php-fpm php81-php-gd php81-php-json php81-php-mbstring php81-php-mysqlnd php81-php-xml php81-php-xmlrpc php81-php-opcache php-mbstring php-dom php-gd php-zip php-xdebug -y \
    && yum install curl php-json php-bcmath php-common php-devel php-gd php-mysqlnd php-pdo php-pear php-pecl-apcu php-pecl-zip php-process php-soap php-xml php-mbstring php-dom php-zip skopeo php-cli -y \
    && sed -i "s/memory_limit = 128M/memory_limit = -1/" /etc/php.ini \
    && sed -i "\$ a xdebug.mode=coverage" /etc/php.ini \
    && wget https://getcomposer.org/installer \
    && php installer --install-dir=/usr/local/bin --filename=composer \
    && rm -rf installer \
    php -v
USER 1001