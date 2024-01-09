# Ubuntu-WEB-Server

## Kurulum

İlk önce apacheyi indiriyoruz

```
apt install apach2 -y
```

Apache indirildikten sonra servisimizi aktif ediyoruz


```
systemctl enable --now apache2
```


Apache servisimizi başlattıktan sonra `systemctl status apache2` yazarak servisimizin durumunu kontrol ediyoruz bir problem yoksa devam ediyoruz.


Gerekli Firewall izinlerini ayarlıyoruz

```
ufw enable # FW yi aktif ediyoruz
ufw allow ssh # SSH iznini veriyoruz
ufw allow apache # Apache iznini veriyoruz
```

Tarayıcımıza sunucumuzun IP adresini yazıp test ediyoruz.

![image](https://github.com/ugurcomptech/Ubuntu-WEB-Server/assets/133202238/7101a86d-8da2-42e7-81d3-a37ea705babe)



Apache Dizinleri (Web Dosyaları)

Görmüş olduğumuz test page sayfasının dosya yoluna gidiyoruz

```
root@master:/home/master# nano /var/www/html/index.html
```

İçerisini açtığınızda test sayfasının HTML kodlarını göreceksiniz. HTML bilmemize gerek yok biz sadece Web dosyalarını değiştireceğiz. Googleye `basic html` yazarsanız githubda bazı html sayfaları bulabilirsiniz. Eğer kendi repolarınızda varsa bunlarıda kullanabilirsiniz. Ben githubdan bir tane buldum sizlerde bunu kullanabilirsiniz.

Serverımıza gerekli html dosyalarını indiriyoruz:

```
git clone https://github.com/designmodo/html-website-templates.git
```

Repo indirildikten sonra gerekli dizine gidiyoruz ve aşağıdaki komudu yazıyoruz:

```
root@master:/home/master/html-website-templates/Animated Landing Page Website Template# cp -r * /var/www/html/
```

/var/www/html/ içerisindeki index.html dosyasının üzerine yazacaktır. 

Tarayıcımızda Test Edelim:

![image](https://github.com/ugurcomptech/Ubuntu-WEB-Server/assets/133202238/29c32bad-dd52-4e85-8a30-4e3404ce68dc)


## Virtualhost 

Apache web sunucu yazılımı, birden fazla web sitesini aynı fiziksel sunucu üzerinde barındırmak için "Virtual Host" özelliğini destekler. Virtual Host, aynı IP adresi veya portu kullanarak farklı alan adlarına veya alt alan adlarına hizmet verilmesini sağlar.

İlk önce `/var/www/` altında bir tane dosya oluşturacağız.

```
mkdir -p /var/www/sirket1.com/dosyalar
```
sirket1.com'un olduğunu belirttik ve onun altına bir klasör daha açtık. Şimdi gerekli izinleri vereceğiz:

```
chown -R www-data: /var/www/sirket1.com/
chmod -R 755 /var/www/sirket1.com/
```

Gerekli izinleri halettikten sonra şimdi `index.html` dosyası oluşturacağız:

```
nano /etc/www/sirket1.com/dosyalar/index.html
```

Dosyamızı oluşturduktan sonra sirket1.com.conf adında bir config dosyası oluşturacağız:

```
nano /etc/apache2/sites-enabled/sirket1.com.conf
```

İçerisini açtığınızda boş bir conf dosyası gelecektir. CTRL+R tuşuna basarak `/etc/apache2/sites-available/000-default.conf` dosyasını buraya aktarabilirsiniz.

sirket1.com.conf dosyası:

```
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/sirket1.com/dosyalar # Dosya yolunu buraya yazıyoruz

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```


Config dosyamızı test etmek için `apache2ctl configtest` komutunu yazıyoruz. **Syntax OK** yazıyorsa eğer bir sorun yok demektir.

Eski config dosyamızı `a2dissite 000-default.conf` yazarak disabled ediyoruz.

Yeni config dosyamızı `e2ensite sirket1.com.conf` yazarak enabled ediyoruz.

Apache servisini `systemctl restart apache2` yazarak yeniden başlatıyoruz.

Tarayıcımıza gelip kontrol ediyoruz:

![image](https://github.com/ugurcomptech/Ubuntu-WEB-Server/assets/133202238/f274b4ef-181b-433e-a930-dd7244628c24)
























