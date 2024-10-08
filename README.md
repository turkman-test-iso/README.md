# Turkman Linux notlarım: 

# 1- Kurulum sonrası işlemler:
Turkman Linux kurulum sonrası terminali açalım ve aşağıdaki komutlarla depomuzu güncelleyelim: (root ile)
```
ymp repo --update
```

Depodaki güncellenen paketleri görmek için:
```
ymp it --update
```

Depoda güncellenen paketleri kurmak için:
```
ymp it --upgrade --no-emerge
```

Depodan paket kurmak için:
it veya install komutu kullanılır

Örnek:
ymp it xarchiver (Kaynak koddan paket kurulum için)
ymp it xarchiver --no-emerge (Depodan derlenmiş .ymp paketi kurmak için)

Kurulu paketi kaldırmak için rm veya remove komutu kullanılır:
ymp remove xarchiver

# 2- Turkman Linux zaman dilimini ayarlama: 
Terminal den aşağıdaki komutu girelim örnek olarak ben İstanbul'u aldım (rootlu)

```
ymp install tzdata --no-emerge
rm /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Istanbul /etc/localtime

```
veya
rm /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Istanbul /etc/localtime

# 3- Turkman Linux Flatpak kurulumu ve kullanımı:

Flatpak kuralım: (rootlu)
```
ymp install flatpak --no-emerge
```

Servisleri açalım:
```
rc-update add devfs
rc-update add fuse
rc-update add hostname

```

root dan exit komutu ile çıkalım

Flatpak depo ekleyelim: (rootsuz)
```
flatpak --user remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

Bilgisayarı yeniden başlatalım.

Önemli Not: Flatpak paketlerinin kurulumu, kaldırılması yada güncellenmesi rootsuz yapılır!

https://flathub.org/ sitesine giriş yapıp kurmak istediğimiz uygulamanın manuel install komutunu kopyalayıp terminale yazılım:
Örnek flatpak uygulama kurulumu: 
flatpak install flathub org.gimp.GIMP

Kurulu olan bir flatpak uygulamasını kaldırma:
flatpak uninstall flathub org.gimp.GIMP

Flatpak paketleri güncelleme:
Tek paket için:
flatpak update package_name
Tüm paketler için:
flatpak update

Flatpak paket arama:
flatpak search paket_ismi

Paketleri listeleme:
flatpak list

Bozuk paketleri onarma:
flatpak repair

Flatpak kurulduğundan bu yana yapılan değişiklikleri görme:
flatpak history

Fleatseal kurarak flatpak uygulamalarımızın izinlerini yönetelim:
flatpak install flathub com.github.tchx84.Flatseal
(Flatseal, Flatpak uygulamalarınızdaki izinleri gözden geçirmek ve değiştirmek için kullanılan grafiksel bir yardımcı programdır.)

# 4- Turkman Linux AppImage nasıl çalıştırılır?

AppImage için aşağıdaki komutu girelim. (rootlu)
```
ymp install fuse fuse2 --no-emerge
rc-update add fuse
rc-service fuse start
modprobe fuse
mount -t fusectl none /sys/fs/fuse/connections
chmod u+s /usr/bin/fusermount

```

Gear Lever uygulamasını flatpaktan indirip AppImage uygulamalarımızı pratik bir şekilde kullanabiliriz. (Rootsuz)
flatpak install flathub it.mijorus.gearlever


AppImage Manuel kurulumu ise:

AppImage için izin verelim : chmod +x file_name.AppImage
Çalıştırmak için : çift tıkla yada ./file_name.AppImage

Örnek Desktop Entry dosya yapımı:
[Desktop Entry]
Name=QMPlay2
Exec=/path/to/qmplay2.AppImage
Icon=QMPlay2
Type=Application
Terminal=false
Categories=AudioVideo;Audio;Video;

# 5- Turkman Linux bluetooth etkinleştirme ve aygıtı bağlama: 
Bluetooth aygıtlarımızı aşağıdaki komutla bağlantı yapabiliriz (Rootlu)

```
rc-update add bluetooth 
rc-service bluetooth start
modprobe uhid

```

Bluetooth kullanım komutları: 

1- bluetoothctl scan on (Aygıt tarama)

2- bluetoothctl connect Mac Address (Aygıta bağlanmak için):
bluetoothctl connect E2:4E:41:13:3B:24

3- bluetoothctl disconnect Mac Address (Aygıt bağlantısını kesme):
bluetoothctl disconnect E2:4E:41:13:3B:24

4- bluetoothctl trust Mac Address (Aygıta kalıcı bağlanmak için)
bluetoothctl trust E2:4E:41:13:3B:24

https://flathub.org/apps/io.emeric.toolblx (Mac adresi tespiti için güzel bir gui uygulama)
