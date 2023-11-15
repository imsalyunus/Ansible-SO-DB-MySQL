Tricks for Linux:

#Perintah untuk Mengedit sebuah text didalam file
sed -ie 's/<nama yang dicari>/<nama yang diganti>/' <nama filenya>

#/bin/bash -xe
sudo apt-get update -y && sudo apt-get upgrade -y
sudo apt-get install apache2 php php-mysql mysql-server -y

# TODO: validasi apakah apache2 sudah install atau belum?
sudo systemctl restart apache2
cd /var/www/html/
pwd

sudo git clone https://github.com/sdcilsy/sosial-media.git
# TODO: if else pengecekan apakah ada folder sosial-media atau tidak?
SOSIAL_MEDIA=$(ls | grep sosial-media | wc -l)

if [[ SOSIAL_MEDIA -eq 1 ]]; then
    echo "berhasil"
elif [[ SOSIAL_MEDIA -ne ]]; then
    exit(1)
fi

sudo mysql -uroot -e "create user 'devopscilsy'@'localhost' identified by '1234567890';"
sudo mysql -uroot -e "grant all privilages on . to 'devopscilsy'@'localhost';"
sudo mysql -uroot -e "create database dbsosmed;"
sudo mysql -uroot -e "create user 'wordpress'@'localhost' identified by '1234567890';"
sudo mysql -uroot -e "grant all privilages on . to 'wordpress'@'localhost';"
sudo mysql -uroot -e "create database dbwordpress;"
cd /var/www/html/
pwd

sudo mysql -udevopscilsy -p1234567890 dbsosmed < dump.sql
sudo git clone https://github.com/WordPress/WordPress.git
# TODO: if else pengecekan apakah ada folder WordPress atau tidak?
WORDPRESS=$(ls | grep WordPress| wc -l)

if [[ WORDPRESS -eq 1 ]]; then
    echo "berhasil"
elif [[ WORDPRESS -ne ]]; then
    exit(1)
fi
sudo mv /var/www/html/WordPress /var/www/html/wordpress
cd /var/www/html/wordpress
pwd

sed -ie 's/database_name_here/db_wordpress/' wp-config.php
sed -ie 's/username_here/wp-user/' wp-config.php
sed -ie 's/password_here/wp-pass123/' wp-config.php
sed -ie 's/localhost/$(curl -s http://169.254.169.254/latest/meta-data/local-ipv4)/' wp-config.php

sudo git clone https://github.com/sdcilsy/landing-page.git
# TODO: if else pengecekan apakah ada folder landing-page atau tidak?
LANDING_PAGE=$(ls | grep landing-page | wc -l)

if [[ LANDING_PAGE -eq 1 ]]; then
    echo "berhasil"
elif [[ LANDING_PAGE -ne ]]; then
    exit(1)
fi
sudo systemctl restart apache2
