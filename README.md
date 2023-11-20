# Jarkom-Modul-3-IT18-2023

# Lapres (Laporan Resmi)

    1. Keisya Nabila Zahra    (5027211058)
    2. Auditya Maulana Adnan  (5027211068)

# Laporan Resmi Praktikum Modul 3 Jarkom

## Soal 1

Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.

Semua **CLIENT** harus menggunakan konfigurasi dari DHCP Server.

---

Set konfigurasi 

**********Aura********** 

```bash
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.242.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.242.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.242.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.242.4.1
	netmask 255.255.255.0
```

**************Himmel************** 

```bash
auto eth0
iface eth0 inet static
	address 192.242.1.2
	netmask 255.255.255.0
	gateway 192.242.1.1
```

**Heiter** 

```bash
auto eth0
iface eth0 inet static
	address 192.242.1.3
	netmask 255.255.255.0
	gateway 192.242.1.1
```

**************Denken************** 

```bash
auto eth0
iface eth0 inet static
	address 192.242.2.2
	netmask 255.255.255.0
	gateway 192.242.2.1
```

************Eisen************ 

```bash
**auto eth0
iface eth0 inet static
	address 192.242.2.3
	netmask 255.255.255.0
	gateway 192.242.2.1**
```

********Lugner******** 

```bash
auto eth0
iface eth0 inet static
	address 192.242.3.2
	netmask 255.255.255.0
	gateway 192.242.3.1
```

************Linie************ 

```bash
auto eth0
iface eth0 inet static
	address 192.242.3.3
	netmask 255.255.255.0
	gateway 192.242.3.1
```

************Lawine************

```bash
auto eth0
iface eth0 inet static
	address 192.242.3.4
	netmask 255.255.255.0
	gateway 192.242.3.1
```

**************Richter, Revolte, Sein, Stark**************

```bash
auto eth0
iface eth0 inet dhcp
```

**************Frieren**************

```bash
auto eth0
iface eth0 inet static
	address 192.242.4.4
	netmask 255.255.255.0
	gateway 192.242.4.1
```

**************Flamme************** 

```bash
auto eth0
iface eth0 inet static
	address 192.242.4.5
	netmask 255.255.255.0
	gateway 192.242.4.1
```

******Fern****** 

```bash
auto eth0
iface eth0 inet static
	address 192.242.4.6
	netmask 255.255.255.0
	gateway 192.242.4.1
```

**********************Lakukan instalasi DHCP Relay********************** 

```bash
apt-get update
apt install isc-dhcp-relay -y
```

masukkan konfigurasi ini ke /etc/default/isc-dhcp-relay

```bash
# Defaults for isc-dhcp-relay initscript
# sourced by /etc/init.d/isc-dhcp-relay
# installed at /etc/default/isc-dhcp-relay by the maintainer scripts

#
# This is a POSIX shell fragment
#

# What servers should the DHCP relay forward requests to?
SERVERS="192.242.1.2"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth1 eth3 eth2 eth4"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""

> /etc/default/isc-dhcp-relay
```

lalu restart dhcp relay 

```bash
service isc-dhcp-relay restart
```

hasil :

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled.png)

**********************Lakukan instalasi DHCP Server********************** 

```bash
apt-get update
apt install isc-dhcp-server -y
```

masukkan konfigurasi ini ke /etc/default/isc-dhcp-server

```bash
# Defaults for isc-dhcp-server (sourced by /etc/init.d/isc-dhcp-server)

# Path to dhcpd's config file (default: /etc/dhcp/dhcpd.conf).
#DHCPDv4_CONF=/etc/dhcp/dhcpd.conf
#DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf

# Path to dhcpd's PID file (default: /var/run/dhcpd.pid).
#DHCPDv4_PID=/var/run/dhcpd.pid
#DHCPDv6_PID=/var/run/dhcpd6.pid

# Additional options to start dhcpd with.
#<----->Don't use options -cf or -pf here; use DHCPD_CONF/ DHCPD_PID instead
#OPTIONS=""

# On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
#<----->Separate multiple interfaces with spaces, e.g. "eth0 eth1".
INTERFACESv4="eth0"
INTERFACESv6="eth0"
```

lalu restart dhcp server 

```bash
service isc-dhcp-server restart
```

hasil :

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%201.png)

---

## Soal 2

Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80 **(2)**

---

untuk setting prefix IP kita dapat menambahkan kode ini ke DHCP Server di /etc/dhcp/dhcpd.conf

```bash
subnet 192.242.3.0 netmask 255.255.255.0 {
    range  192.242.3.16 192.242.3.32;
    range  192.242.3.64 192.242.3.80;
    option routers 192.242.3.1;
    option broadcast-address 192.242.3.255;
    option domain-name-servers 192.242.1.3;
    default-lease-time 180; 
    max-lease-time 5760;
}
```

hasil ;

Revolte

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%202.png)

Ritcher 

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%203.png)

---

## Soal 3

Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 **(3)**

---

untuk setting prefix IP kita dapat menambahkan kode ini ke DHCP Server di /etc/dhcp/dhcpd.conf

```bash
subnet 192.242.4.0 netmask 255.255.255.0 {
    range  192.242.4.12 192.242.4.20;
    range  192.242.4.160 192.242.4.168;
    option routers 192.242.4.1;
    option broadcast-address 192.242.4.255;
    option domain-name-servers 192.242.1.3;
    default-lease-time 720;
    max-lease-time 5760;
}
```

hasil : 

Sein

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%204.png)

Stark

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%205.png)

---

## Soal 4

Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut **(4)**

---

Agar semua client dapat terhubung ke internet konfigurasi pada file /etc/bind/named.conf.options pada Heiter (DNS SERVER)

```bash
options {
        directory \"/var/cache/bind\";

        forwarders {
                8.8.8.8;
                8.8.8.4;
        };

        // dnssec-validation auto;
        allow-query { any; };
        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};
```

Hasil :

Stark

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%206.png)

Sein

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%207.png)

Richter

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%208.png)

Revolte

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%209.png)

---

## Soal 5

Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit **(5)**

---

```bash
subnet 192.242.3.0 netmask 255.255.255.0 {
    ...
    default-lease-time 180; 
    max-lease-time 5760;
    ...
}
subnet 192.242.4.0 netmask 255.255.255.0 {
    ...
    default-lease-time 720;
    max-lease-time 5760;
    ...
}
```

hasil :

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2010.png)

---

## Soal 6

>Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

Sebelum menyetting nginx ada perlunya untuk mendownload resource yang telah diberikan di soal menggunakan `wget`


```
apt install wget unzip -y
mkdir /var/www/granz.channel.IT18
chown -R www-data:www-data /var/www/granz.channel.IT18
cd /var/www/granz.channel.IT18
wget https://cloud.amayuuki.my.id/api/public/dl/xbeUirGo/my_data/granz.channel.IT18.com.zip
unzip -e *
rm *.zip
```

### Script
setelah melakukan download resource beserta unzip maka dilanjutkan dengan mengkonfigurasi `nginx` sebagai berikut

```
echo "
server {
    listen 80;
    server_name _;
    root /var/www/granz.channel.IT18;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
    }
} " > /etc/nginx/sites-available/granz.channel.IT18.com

ln -s /etc/nginx/sites-available/granz.channel.IT18.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

service nginx restart
```

### Output

Jalankan command `lynx localhost` pada masing2 worker dan akan muncul hasil sebagai berikut


![image6](https://github.com/aud1tya4dnan/Jarkom-Modul-3-IT18-2023/assets/91017662/d2074868-8e18-44c9-b301-9bf178bdbb9b)


## Soal 7

>Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
Lawine, 4GB, 2vCPU, dan 80 GB SSD.
Linie, 2GB, 2vCPU, dan 50 GB SSD.
Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

Sebelum mulai mengerjakan soal7 diperlukan untuk melakukan setup awal, kemudian mengkonfigurasi load balancer pada Eisen

### Script

Sebelum mengkonfigurasi Eisen perlu dilakukan konfigurasi pada Heiter Sebagai DNS servernya
```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.it18.com. root.riegel.canyon.it18.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.it18.com.
@       IN      A       192.173.2.3     ; IP LB Eiken
www     IN      CNAME   riegel.canyon.it18.com.' > /etc/bind/jarkom/riegel.canyon.it18.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.it18.com. root.granz.channel.it18.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.it18.com.
@       IN      A       192.173.2.3     ; IP LB Eiken
www     IN      CNAME   granz.channel.it18.com.' > /etc/bind/jarkom/granz.channel.it18.com
```

kemudian melakukan konfigurasi pada Eisen (load balancer) 
```
echo '
#Default menggunakan Round Robin
upstream worker  {
server 192.168.3.4; #IP Lawine
server 192.168.3.3; #IP Linie
server 192.168.3.2; #IP Lugner
}

server {
    listen 80;
    server_name granz.channel.it18.com www.granz.channel.it18.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;


    location / {
        proxy_pass http://worker;
        proxy_set_header    X-Real-IP $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    Host $http_host;
    }
} ' > /etc/nginx/sites-available/granz.channel.it18.com

ln -s /etc/nginx/sites-available/granz.channel.it18.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

service nginx restart
```

Kemudian diakses pada salah satu client, yang kami gunakan adalah revolte

### Output

Jalankan command berikut pada `Revolte`
```
ab -n 1000 -c 100 http://www.granz.channel.it18.com/
```

Hasilnya adalah sebagai berikut

![image12](https://github.com/aud1tya4dnan/Jarkom-Modul-3-IT18-2023/assets/91017662/ac8098b7-b470-40c5-9aad-bc5c8af219b6)

## Soal 8

>Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
- a. Nama Algoritma Load Balancer
- b. Report hasil testing pada Apache Benchmark
- c. Grafik request per second untuk masing masing algoritma. 
- d. Analisis

Untuk konfigurasinya kurang lebih sama dengan nomer7 

Untuk grimore nya kami membuatnya di google docs
https://docs.google.com/document/d/1A2zuaRRg-M-25joBtuUKaR3IBic--NRxm6XlNUDUKgg/edit?usp=sharing

### Output

Gunakan command pada client revolte
```
ab -n 200 -c 10 http://www.granz.channel.it18.com/ 
```

**Round Robin**

[IMAGE]

**Least Connection**

[Image]

**IP Hash**

[Image]

** Generation Hash**

[Image]

**Grafik**

[Image]


## Soal 9

>Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.

Lakukan testing pada Load balancer `Eisen` yang telah di konfigurasi sebelumnya, setelah itu dirubah pada bagian `upstream worker` menjadi `3 Worker`, `2 Worker`, dan `1 Worker`

Kemudian jalankan command pada client `Revolte` 
```
ab -n 100 -c 10 http://www.granz.channel.it18.com/ 
```

### Output

**3 Worker**

[IMAGE]

**2 Worker**

[Image]

**1 Worker**

[Image]

**Grafik**

[Image]

## Soal 13

Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern. **(13)**

---

Pertama-tama pada denken lakukan instalasi sebagai berikut 

```bash
apt-get update
apt-get install mariadb-server -y
```

setelah itu jangan lupa untuk start mysql sebelum digunakan dengan command dibawah

```bash
service mysql start
```

bukalah mysql dengan command ‘mysql’ dan jalankan perintah berikut 

```bash
CREATE USER 'kelompokIT18'@'%' IDENTIFIED BY 'passwordIT18';
CREATE USER 'kelompokIT18'@'localhost' IDENTIFIED BY 'passwordIT18';
CREATE DATABASE dbkelompokIT18;
GRANT ALL PRIVILEGES ON *.* TO 'kelompokIT18'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokIT18'@'localhost';
FLUSH PRIVILEGES;
```

setelah itu masukkan command berikut pada /etc/mysql/my.cnf agar client dapat mengakses database

```bash
[mysqld]
skip-networking=0
skip-bind-address

Service my
SELECT user, host FROM mysql.user;
```

Setelah itu bukalah client dan lakukan instalasi berikut 

```bash
apt-get update
apt-get install mariadb-client -y
```

jalankan command berikut untuk mengakses database

```bash
mariadb --host=192.242.2.2 --port=3306 --user=kelompokIT18 --password
```

hasil : 

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2011.png)

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2012.png)

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2013.png)

---

## Soal 14

Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan [quest guide](https://github.com/martuafernando/laravel-praktikum-jarkom) berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer **(14)**

---

lakukan instalasi berikut pada worker laravel 

```bash
apt-get update
apt-get install -y lsb-release ca-certificates apt-transport-https software-properties-common gnupg2
curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

apt-get update
apt-get install php8.0-mbstring php8.0-xml php8.0-cli php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
apt-get install nginx -y

apt-get update
apt-get install lynx -y
```

setelah selesai lakukan instalasi composer dan gitclone

```bash
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/bin/composer

apt-get install git -y
cd /var/www
git clone https://github.com/martuafernando/laravel-praktikum-jarkom.git
cd /var/www/laravel-praktikum-jarkom/
composer update
composer install
```

setelah itu lakukan konfigurasi ini pada worker

```bash
cp .env.example .env

echo '
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=192.242.2.2
DB_PORT=3306
DB_DATABASE=dbkelompokIT18
DB_USERNAME=kelompokIT18
DB_PASSWORD=passwordIT18

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
' > /var/www/laravel-praktikum-jarkom/.env

cd /var/www/laravel-praktikum-jarkom && php artisan migrate:fresh
cd /var/www/laravel-praktikum-jarkom && php artisan db:seed --class=AiringsTableSeeder
cd /var/www/laravel-praktikum-jarkom && php artisan key:generate
cd /var/www/laravel-praktikum-jarkom && php artisan jwt:secret
cd /var/www/laravel-praktikum-jarkom && php artisan storage:link
```

jika berhasil lakukan konfigurasi ini pada masing2 worker 

********Fern********

```bash
echo '
server {

    listen 8001;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}
' > /etc/nginx/sites-available/implementasi

ln -s /etc/nginx/sites-available/implementasi /etc/nginx/sites-enabled/
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```

****Flamme****

```bash
echo '
server {

    listen 8002;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}
' > /etc/nginx/sites-available/implementasi

ln -s /etc/nginx/sites-available/implementasi /etc/nginx/sites-enabled/
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```

**Frieren** 

```bash
echo '
server {

    listen 8003;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}
' > /etc/nginx/sites-available/implementasi

ln -s /etc/nginx/sites-available/implementasi /etc/nginx/sites-enabled/
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```

setelah itu untuk testing jalankan command berikut 

```bash
lynx localhost:{Port}
```

Hasil :

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2014.png)

******Frieren****** 

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2015.png)

Flamme

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2016.png)

**********Fern********** 

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2017.png)

---

## Soal 15

Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.

POST /auth/register**(15)**

---

Sebelum memulai lakukan instalasi ini pada client 

```bash
apt-get update
apt-get install lynx -y
apt-get install htop -y
apt-get install apache2-utils -y
apt-get install jq -y
```

setelah itu masukkan script berikut pada register.json 

```bash
echo '
{
  "username": "kelompokIT18",
  "password": "passwordIT18"
}
' > register.json
```

untuk mengecek hasil, jalankan command berikut 

```bash
ab -n 100 -c 10 -p register.json -T application/json http://192.242.4.6:8001/api/auth/register
```

Hasil :

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2018.png)

Penjelasan :

- Requests per second (RPS): 78.22 RPS merupakan jumlah rata-rata permintaan yang berhasil diproses setiap detik.
- Failed requests: Dari 100 permintaan, 99 mengalami kegagalan, semuanya terkait dengan panjang respons (Length: 99).
- Time per request: Rata-rata waktu yang dibutuhkan untuk menanggapi setiap permintaan adalah 127.846 ms.
- Connection Times: Waktu tercepat untuk menghubungkan adalah 0 ms, waktu terlama adalah 1 ms. Waktu pemrosesan berkisar antara 37 ms hingga 166 ms.
- Percentage of Requests Served within a Certain Time: Menunjukkan distribusi waktu respons. Sebagai contoh, 50% dari permintaan diproses dalam waktu kurang dari 115 ms.

## Soal 16

Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire

POST /auth/login **(16)**

---

tambahkan script berikut ke file login.json

```bash
{
  "username": "kelompokIT18",
  "password": "passwordIT18"
}
' > login.json
```

untuk mengecek hasil jalankan command berikut 

```bash
ab -n 100 -c 10 -p login.json -T application/json http://192.242.4.6:8001/api/auth/login
```

Hasil  :

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2019.png)

Penjelasan :

- Requests per second (RPS): 21.68 RPS merupakan jumlah rata-rata permintaan yang berhasil diproses setiap detik. Ini lebih rendah dibandingkan dengan pengujian sebelumnya.
- Failed requests: Dari 100 permintaan, 40 mengalami kegagalan, semuanya terkait dengan panjang respons (Length: 40).
- Time per request: Rata-rata waktu yang dibutuhkan untuk menanggapi setiap permintaan adalah 461.224 ms.
- Connection Times: Waktu tercepat untuk menghubungkan adalah 0 ms, waktu terlama adalah 2 ms. Waktu pemrosesan berkisar antara 62 ms hingga 878 ms.
- Percentage of Requests Served within a Certain Time: Menunjukkan distribusi waktu respons. Sebagai contoh, 50% dari permintaan diproses dalam waktu kurang dari 635 m

---

## Soal 17

Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire

GET /me **(17)**

---

untuk melakukan ini pertama2 jalankan script ini yang mengarahkan hasil ke login_output.txt

```bash
curl -X POST -H "Content-Type: application/json" -d @login.json http://192.242.4.6:8001/api/auth/login > login_output.txt
```

kemudian jalankan command berikut untuk mendapat token 

```bash
token=$(cat login_output.txt | jq -r '.token')
```

untuk melakukan pengecekan jalankan command berikut 

```bash
ab -n 100 -c 10 -H "Authorization: Bearer $token" http://192.242.4.6:8001/api/me
```

Hasil :

![Untitled](praktikum%203%204eaad37b4d394bd8b1123ba27e94a074/Untitled%2020.png)

Penjelasan :

- Requests per second (RPS): 68.32 RPS merupakan jumlah rata-rata permintaan yang berhasil diproses setiap detik. Ini merupakan peningkatan signifikan dibandingkan dengan pengujian sebelumnya.
- Failed requests: Dari 100 permintaan, 38 mengalami kegagalan, semuanya terkait dengan panjang respons (Length: 38).
- Time per request: Rata-rata waktu yang dibutuhkan untuk menanggapi setiap permintaan adalah 146.379 ms.
- Connection Times: Waktu tercepat untuk menghubungkan adalah 0 ms, waktu terlama adalah 2 ms. Waktu pemrosesan berkisar antara 31 ms hingga 218 ms.
- Percentage of Requests Served within a Certain Time: Menunjukkan distribusi waktu respons. Sebagai contoh, 50% dari permintaan diproses dalam waktu kurang dari 141 ms.
