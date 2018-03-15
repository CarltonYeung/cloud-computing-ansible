Make sure hosts file contains the right machines

Run ansible with python3
ansible-playbook sample-playbook.yml -e 'ansible_python_interpreter=/usr/bin/python3'

1. install-apache-php.yml
2. install-mongodb.yml
3. install-postfix.yml
4. deploy-hw0.yml
5. deploy-wp2.yml

.htaccess doesn't work without configuring /etc/apache2/apache2.conf
Set AllowOverride All for /var/www

####################################
# Getting MongoDB to work with PHP #
####################################
1. Install phpize
   sudo apt install php7.0-dev

2. Install pecl
   sudo apt install php-pear

3. Install MongoDB PHP Driver
   sudo pecl install mongodb

4. Configure php.ini
   echo "extension=mongodb" >> /etc/php/7.0/apache2/php.ini

5. Install composer
   sudo apt install composer

6. Install PHP Library for MongoDB (PHPLIB)
   This step will install dependencies (mongodb/mongodb)
   Inside /ttt, run:
   sudo composer require mongodb/mongodb --ignore-platform-reqs




install-mysql.yml
use python2
ansible-playbook sample-playbook.yml -e 'ansible_python_interpreter=/usr/bin/python'
