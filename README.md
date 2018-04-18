# cilog
Aplikasi untuk membantu membuka log apa yang dibuka oleh client mikrotik router di database linux Ubuntu.

Konfigurasi di Mikrotik dan Linux Ubuntu
----------------------------------------

Dikondisikan sebelumnya sudah membuat NAT di Mikrotik. 

Di Winbox

IP -> Firewall -> NAT -> +

General
-------
Chain: dstnat

Protocol: 6(TCP)

Dst. Port: 80

Action
------

Action: redirect

To Ports: 8080

OK


Setelah di atas selesai maka aktifkan proxy
-------------------------------------------

IP -> Web Proxy

General
-------
Enabled dicentang 

OK

Mengaktifkan LOG agar bisa dikirimkan ke linux ubuntu
-----------------------------------------------------


Log Action
---------- 
System -> Logging -> Actions -> +

Name: Action1

Type: remote

Remote Address: ip addresss linux ubuntu

OK

Log Rule
--------

System -> Logging -> Rules -> +

Rules
----- 

Topics: Web-proxy (arah panah ke bawah di klik) lalu !Debug
        
Prefix dikosongkan

Action: Action1

OK

Installasi dan konfigurasi untuk mendukung disimpannya log pada database mysql
------------------------------------------------------------------------------


Ubuntu 16.04.4 LTS
------------------

Installasi :

apt-get install apache2

apt-get install phpmyadmin

apt-get install mysql-server

apt-get install rsyslog

apt-get install rsyslog-mysql

nano /etc/rsyslog.conf

Hilangkan tanda # pada module(load="imudp")

Hilangkan tanda # pada input(type="imudp" port="514")

Hilangkan tanda # pada modul(load="imtcp")

Hilangkan tanda # pada input(type-"imtcp" port="514")

Tambahkan agar masuk di /var/log/mikrotik.log : :fromhost-ip,isequal,"ipgatewaymikrotik" /var/log/mikrotik.log

Memasukkan cilog ke web server
------------------------------

cd /var/www/html

git clone https://github.com/kurniawandata/cilog.git

cd /var/www/html/cilog

nano mikrolog.php

Isi username dan password database yang digunakan lalu simpan

Mengakses Cilog
---------------

http://ip address web/cilog/


Program cilog dan tutorial ini dibuat oleh :
--------------------------------------------

Kurniawan. trainingxcode@gmail.com. 

xcode.or.id
