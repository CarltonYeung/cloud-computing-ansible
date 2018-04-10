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



Install Ansible
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible

WEB SERVER
ansible-playbook setup-laravel.yml -e 'ansible_python_interpreter=/usr/bin/python3'; ansible-playbook install-postfix.yml -e 'ansible_python_interpreter=/usr/bin/python3'
sudo git init && sudo git remote add origin https://CarltonYeung@bitbucket.org/CarltonYeung/cse-356-course-project.git && sudo git fetch --all && sudo git reset --hard origin/master
sudo git fetch origin && sudo git merge origin/master
sudo composer install

.env
MAIL_DRIVER=smtp
MAIL_HOST=smtp.googlemail.com
MAIL_PORT=465
MAIL_USERNAME=cayeung.cse356@gmail.com
MAIL_PASSWORD=
MAIL_ENCRYPTION=ssl

MYSQL SERVER
ansible-playbook install-mysql.yml
ansible-playbook install-mysql.yml -e 'ansible_python_interpreter=/usr/bin/python3'
GRANT ALL ON *.* TO 'carlton'@'%' IDENTIFIED BY 'cse356cloudcomputingtwitir' WITH GRANT OPTION;


MONGODB SERVER
ansible-playbook install-mongodb.yml -e 'ansible_python_interpreter=/usr/bin/python3'
use twitir
Configure security group
