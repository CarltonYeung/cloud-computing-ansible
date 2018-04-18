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



CASSANDRA
sudo add-apt-repository ppa:webupd8team/java
sudo apt update && sudo apt install oracle-java8-installer -y
echo "deb http://www.apache.org/dist/cassandra/debian 22x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
curl https://www.apache.org/dist/cassandra/KEYS | sudo apt-key add -
sudo apt update && sudo apt install cassandra -y
nodetool status
wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/cassandra/v2.8.1/cassandra-cpp-driver-dbg_2.8.1-1_amd64.deb; wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/cassandra/v2.8.1/cassandra-cpp-driver-dev_2.8.1-1_amd64.deb; wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/cassandra/v2.8.1/cassandra-cpp-driver_2.8.1-1_amd64.deb; wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/dependencies/libuv/v1.18.0/libuv-dbg_1.18.0-1_amd64.deb; wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/dependencies/libuv/v1.18.0/libuv-dev_1.18.0-1_amd64.deb; wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/dependencies/libuv/v1.18.0/libuv_1.18.0-1_amd64.deb
sudo dpkg -i libuv-dbg_1.18.0-1_amd64.deb libuv-dev_1.18.0-1_amd64.deb libuv_1.18.0-1_amd64.deb cassandra-cpp-driver-dbg_2.8.1-1_amd64.deb cassandra-cpp-driver-dev_2.8.1-1_amd64.deb cassandra-cpp-driver_2.8.1-1_amd64.deb
sudo apt install libgmp-dev -y && sudo pecl channel-update pecl.php.net && sudo pecl install cassandra
add "extension=cassandra.so" to php.ini files

/etc/cassandra/cassandra.yaml
rpc_address: 0.0.0.0
rpc_port: 9042
broadcast_rpc_address: 130.245.168.216
data_file_directories:
    - /var/lib/cassandra/volume

cqlsh
CREATE KEYSPACE twitir WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 1};
CREATE TABLE twitir.media (id int PRIMARY KEY, filename text, contents blob, type text, size int);
CREATE TABLE twitir.refcounts (id int PRIMARY KEY, refcount counter);


https://docs.datastax.com/en/cassandra/2.1/cassandra/configuration/configCassandra_yaml_r.html
Check disk space "df -h"
/dev/vdb needs to be mounted
https://github.com/naturalis/openstack-docs/wiki/Howto:-Creating-and-using-Volumes-on-a-Linux-instance
sudo lsblk -f
sudo mkfs.ext4 /dev/vdb
mkdir /var/lib/cassandra/volume
sudo mount /dev/vdb /var/lib/cassandra/volume
sudo chown cassandra:cassandra /var/lib/cassandra/volume


sudo apt remove cassandra
sudo apt purge cassandra

Load Balancer w/ NGINX
nginx.conf
    include /etc/nginx/sites-available/load-balancer.conf

load-balancer.conf
upstream twitir {
    ip_hash;
    server 130.245.171.55;
    server 130.245.170.178;
    server 130.245.168.218;
}

server {
    listen 80;
    server_name cayeung.cse356.compas.cs.stonybrook.edu;
    location ~ {
        proxy_pass http://twitir;
        proxy_set_header Host $host;
        proxy_next_upstream error timeout http_500;
    }
}

yahoo availability zone is slow af
