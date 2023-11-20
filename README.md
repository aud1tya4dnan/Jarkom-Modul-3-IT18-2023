# Jarkom-Modul-3-IT18-2023

# Lapres (Laporan Resmi)

    1. Keisya Nabila Zahra    (5027211058)
    2. Auditya Maulana Adnan  (5027211068)

# Laporan Resmi Praktikum Modul 3 Jarkom

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

[Output.png]


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

[OUTPUT]

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
