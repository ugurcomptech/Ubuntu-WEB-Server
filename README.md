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
