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















