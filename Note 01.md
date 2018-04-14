#### Bootloader sistemleri 

- MBR 
    - Hafızanın 512 mb kısmını ifade eder. 
    - İçinde;
        - Bootloader
        - Partial Section
        - Magic Section
            - Bootloader olduğunu belirten asıl yerdir. 
            - 2 Byte alan kaplar
            - Buranın silinmesi bootloader özelliğini kaldırır. 
    - Max 2 TB disk için kullanılabilir.
    - Bu kısım silinirse diğer kısımlar sabit kalırsa bile, bios buranın bootloader bir disk olduğunu anlamaz ve diskten yükleme yapamaz.
- GBT
    - MBR yeni teknolojilerde yetersiz kaldığından dolayı yerine geçmiştir.
    - 2 TB fazlası diskler için de kullanılabilir.
    - Bootloader parçasını birden fazla kopya olarak sakladığı için silinmesi durumunda, yedekten yükleme yapabilir.

#### Disk bölümleri

- Ana dizin `\` kısmıdır.
- Bunun aldındaki her dizin birer disk bölümüdür. 
- Örneğin `\home` dizini bir disk olarak atanırsa, daha sonra format atılsa bile tüm kullanıcı bilgileri bilgisayarda kalmaya devam eder.
- Dosya sistemlerine daha sonra bakılacak!
    - `xfs` performans olarak daha iyidir.
    - `ext4` linuxun genel dosya sistemidir.
        - Daha eskidir.
        - Bazı performans sorunları vardır.
- Linux üzerindeki programlar kütüphaneleri ortak kullanır. Bu yüzden root dizine (`\`) fazla bir yer vermeye pek gerek yoktur.
- Tüm kişisel dosya sistemimiz `\home` dizininde bulunduğu için bu alana daha fazla yer vermek daha mantıklıdır.
- `\swap` kısmı, ram kısmı yetersiz kalma durumda ram için kullanılan alandır.
    - Eklenmezse warning verir, fakat eklenmeden geçilebilir.
- `\var` sürekli değişen işlemler için kullanılır ve eğer hızlı bir disk vb varsa buraya atanabilir.
- `\boot` dosyaların yükleneceği kısımdır. 

#### Sistem katmanları

1. Hardware katmanı
2. Linux çeğirdeği
    - Harware ile GNU araçları arasındaki iletişimi sağlar.
    - GNU araçlarının hardware olaylarından bağımsız olarak çalışmasını sağlar.
    - Driver'lar bu katmandadır.
3. GNU katmanı
    - Linux çeğirdeğine hükmetmek için kullanıdığımız komutları vs. kapsar.
    - `ls`, `mkdir` vs gibi araçları kapsar.
4. Arayüz katmanı
    - `Cinnamon`, `KDE`, `Xfce` gibi

- Çekirdek katmanı olarak Linux dışında kullanılanlar;
    - `nt` > Windows
    - `bsd`
    - `xnu` > MacOs
- GNU katmanı ile Arayüz katmanının toplamına `distro` veya `dağıtım` diyoruz.
    - `Mint`, `CentOs` vs gibi dağıtımlar

#### Dosya sistemi

- /bin
    - Derlenmiş binary dosyaları burda bulunur. 
    - Örneğin `ls`, `copy` gibi 
    - Genellikle bütün sistem kullanıcıların kullanacağı şeyler burda tutulur.
    - bin ismi binary (ikili) nin kısaltmasından gelir.
    - Burada çalıştırılabilir komutların derlenmiş (binary yapısında) halleri bulunur.
    - Sistem için kritik önem taşır ve silinmesi durumunda sisteme herhangi bir komut verilemez.
- /sbin
    - Sadece super user kullanıcıların kullanacağı programlar burda bulunur.
- /dev
    - Sistemde bulunan sistemler ile ilgili dosyaların olduğu kısımdır.
    - Bağlı cihazaları, harddiskleri, cdrom vs gibi araçları buradan görebiliriz.
    - Ayrıca içinde; `random`, `urandom`, `null`, `zero` gibi dosyalar da bulunur.
- /lib ve /lib64
    - Sistem içinde bulunan ortak kullanılan kütüphaneler burda bulunur. (sistem kütüphaneleri)
- /etc
    - Sistemde olan bütün ayarlar dosyalarının bulunduğu kısımdır. 
- /boot
    - Açılış dosyalarını ve Kerneli barındırır.
    - Silinmesi durumunda sistem çalışmaz hale gelir.
- /home
    - Kullanıcıların bilgilerinin ve özel ayarlarının bulunduğu dizindir.
- /root
    - Root kullanıcısının bilgilerinin bulunduğu kısımdır.
    - Home dizini içinde bulunmaz, çünkü home farklı bir yerden çekiliyorsa ve iletişim koparsa, root bundan bağımsız olarak çalışmasına devam eder.
- /media ve /mnt
    - Medya kısımlarını ve bağlı cihazları bulundurur.
- /proc
    - Sanal dosyalar bulundurur.
    - Sistem hakkında anlık bilgi verir.
    - Ram üzeirinde tutulur ve anlık olarak üretilir. 
    - Sistem yönetimi için önemlidir.
- /sys
    - /proc dizinine benzer.
    - Yeni olarak eklenmiştir.
- /temp
    - Geçici dosyaların oluşturulduğu yerdir.
    - Ram üzerinde tutulur. 
    - Kullanıcılar başka kullanıcıların dosyalarını silemez.

#### Komut Satırı

- `echo $SHELL`
    - Hangi shell kullanıldığına bakabiliriz.
- `whoami`
- `pwd` veya `echo $PWD`
- `touch`
    - Dosya yoksa oluşturmaya yarar.
    - Dosya varsa oluşturulma tarihini günceller. 
    - Parametre ayarlarından daha önceki bir tarihte oluşturulmuş gibi gösterilebilir.
    - Dosya uzantısının linux üzerinde bir anlamı yoktur.
    - Bu komutla birden fazla dosya oluşturulabilir.
- `history`
    - Geçmişi gösterir.
    - `-c` ile history silinebilir.
- `ls`
    - Dosya listeler
    - Wildcard kullanılabilir.
        - Örn : `ls d*` > d ile başlayan dosyaları listeler
- `rm`
    - Dosya ve dizin siler.
    - `-f` parametresi force anlamına gelir.
        - Birden fazla dosya silinecek ve her defasında `silmek istiyor musunuz` sorusuna yanıt vermemek için kullanılır.
    - İçi dolu olan dizinler direk rm ile silinemez. `rm -rf` ile silinmesi lazım.
    - `-r` parametresi dizin içindeki tüm alt dizin ve dosyaları silmeye yarar. 
- `mkdir`
    - Dizin oluşturmayı yarar.
- `cat`
    - Dosya içeriğini gösterir
    - `-n` parametresi kullanılarak satır numaraları gösterilir.
- `alias`
    - Komut bir değişkene bir komut atama gibi çalışır. 
    - Kalıcı değildir.
    - Örn : `alias listele="ls -la"` > listele dediğimizde `ls -la` komutu çalışacaktır.
    - Tek başına kullanıldığında daha önce kullanılanları gösterir.
    - `unalias <degisken>` yazılarak daha önce oluşturulmuş alias silinebilir.
    - Herhangi bir komutun başına `\` konulursa o anlık alias kapanmış olur.
- `loadkeys <dil>`
    - Klavye düzenini değiştirir.
    - loadkeys us > ingilizce klavye geçişi
    - loadkeys tr > türkçe klavye geçişi
- `su - <kullanici_adi>`
    - Kullanıcı değiştirir.
    - `ctrl + D` geri çıkış yapar.
- `man <komut>`
    - Komutla ilgili manuel dosyaya ulaşmayı sağlar. 
    - `man -k <komut>` ile arama yapılabilir.
    - `man man` komutu ile manuel kullanımı ile ilgili dökümantasyona ulaşılabilir.
    - Eksik ve linux üstünde gelmeyen dökümanlara (minimal sürümlerinde özellikle) aşağıdaki link aracılığıyla internet üzerinden ulaşılabilir.
        - https://linux.die.net/man/
    - `man <section> <komut>`
        - Bu komut ile farklı section'lar üzerinde komut aranabilir.
        - Section kısmı `man man` içinde bulunabilir.
    - `/` kullanılarak arama yapılabilir.
        - `p` > önceki
        - `n` > sonraki
- `wall <message>`
    - Kullanıcıların diğer kullanıcıların ekranına mesaj göndermesini sağlar. 
- `head <dosya>`
    - Dosyanın ilk 10 satırını gösterir.
    - `-n` parametresiyle gösterilecek satır sayısını verebiliriz.
- `tail <dosya>`
    - Dosyanın son 10 satırını gösterir.
    - `-n` parametresiyle gösterilecek satır sayısını verebiliriz.
    - `-F` komutuyla dosyanın anlık olan değişimleri izlenebilir.
- `logger <message>`
    - Sisteme log basmayı sağlar.
    - `/var/log/messages` kısmından bunlar izlenebilir.
- `less <dosya>`
    - Dosyayı bir terminal penceresi büyüklüğünde açar.
    - Yön tuşları yardımıyla kaydırmayı sağlar.
    - `/` kullanılarak arama yapılabilir.
        - `p` > önceki
        - `n` > sonraki
- `more <dosya>`
    - less e benzer ama daha ilkeldir.
- `script`
    - Yapılan her adımı kaydeder ve dosya olarak kaydeder.
    - Kayıttan çıkmak için `ctrl + D` kullanılır.

#### Dosya İzinleri

- `-rw-rw-r-- 1 serhat serhat 62 Apr 13 12:58 deneme`
- dosya izinleri / / kullanıcı / grup / boyut / değiştirilme tarihi / ismi
- `(-)(rw-)(rw-)(r--)`
    - Type
    - Dosya sahibi hakları
    - Grup hakları
    - Herkesin hakları
- `(rw-)`
    - Read (4)
    - Write (2)
    - Execute (1)
- Dosyanın sayısal haklarını verirken, yanlarındaki sayrıların toplamı verilir. 
    - Örneğin 
    - rw- > 6
    - rwx > 7
    - r-- > 4
    - (rw-)(rw-)(r--) > 664
- Root tüm haklara sahiptir.
- Her dosyanın haklarını sahibi veya root belirler.
- `chmod` komutu 
    - `chmod <sayısal_yetki> <dosya_adı>`
    - Örn : chmod 664 deneme.txt
    - `-R` parametresi kullanılırsa, tüm alt dizinler de dahil değiştirme yapabiliriz.
- Dizin içinde yeni dosya oluşturma veya dosya silme hakkı, dizinin write hakkından gelir!! 
- Dizin aslında bir tablodur.
    - Bu tablonun içinde her bir dosya bir satırı ifade eder. 
    - `.` (Kendisi) ve `..` (üst dizin) de bu dizin içinde birer satırı ifade eder.
    - Dosya ekleme, silme düzenleme; aslında dizin tablosundan bilgileri değiştirme anlamına gelir.
    - Bu yüzden bu işlemleri yapmak için dizinin `w` hakkına ihtiyac vardır.
    - Dizin içindeki dosyalarda hakkımız olsa bile, dizin içinde bu hakkımız yoksa, silme veya isim değiştirme gibi dosya işlemleri yapılamaz.
- Dosyalar oluşturulurken,
    - Default olarak x yetkisi verilmez, tüm kullanıcılar için
- Dizinler oluşturulurken
    - Default olarak tüm kullanıcılara x yetkisi verilir.
- `umask` komutuyla default olarak oluşturulan dosya ve dizin hakları üzerinde değişiklikler yapılabilir.
    - Session bazlıdır. Geçicidir.

#### VI Editörü

- Bir şey yazılacaksa `i` harfine basılması lazım.
- İki temel modu var:
    - `Insert Mode` > i harfine basılarak açılır.
    - `Command Mode` > Esc ile geçilir.
- `:wq` > Kaydet çık
- `:q!` > Kaydetmeden çık.
- Yön tuşları çalışmazsa `H-J-K-L` tuşlarıyla yön geçişlerini yapabiliriz.

#### Kullanıcı Yönetimi

- `adduser <username>` veya `useradd <username>`
    - Yeni kullanıcı eklemeyi sağlar.
- `passwd <username>`
    - Kullanıcıya parola atanması sağlanır.
    - Daha önce parolası varsa bunu değiştirmeyi sağlar.
        - Root dışında diğer kullanıcılara önceki parolasını sorar.
- `su - <username>`
    - Kullanıcı değiştirmeyi sağlar.
- `userdel <user>`
    - Kullanıcı siler.
- Yeni bir kullanıcı oluşturulduğunda;
    - Home dizini altında yeni bir dizin oluşturulur.
    - `/etc/passwd` içinde kullanıcı için bir kayıt oluşturulur. 
    - `/etc/shadow` içinde parola için bir kayıt oluşturulur. 
- `/etc/passwd` içeriği
    - `root:x:0:0:root:/root:/bin/bash`
        - Kullanıcı adı
        - Parola (x) > Başka bir yere taşındı
        - Kullanıcı ID
        - Kullanıcı grup numarası 
        - Açıklama
        - Kullanıcının home dizini
            - Home dizini altında olması gerekmez, başka herhangi bir yer verilebilir.
        - Default terminali
            - `nologin` > Giriş yapamaz.
            - `shutdown` > Giriş yaptığında direk kapanır.
    - Bu dosya içinde root kullanıcı adı değiştirilebilir.
    - Herhangi bir kullanıcının kullanıcı ID bilgisi `0` yapılırsa root olmuş olur.
- `/etc/shadow` içeriği
    - Kullanıcı adı
    - Parola
        - Parolanın `$6` kısmı hash algoritmasını söyler.
        - 6 > SHA512
        - Sonraki iki dolar işareti arasında kalan kısım, hash oluştururken kullanılan `salt` kısmıdır.
            - Bu sayede aynı parolayı kullanan kullanıcıların hash sonuçları farklı çıkar.
        - Parola kısmında ! işareti varsa, o kullanıcıya daha parola atanmadığı anlamına gelir.
    - Kullanıcının bitiş süresi
    - Giriş süresinin bitiş tarihi
    - Kaç gün sonra tekrar parola değiştirmesini isteyeceği 
    - ... gibi bilgiler burada belirlenir.
- Shadow ve Passwd dosyalarının son düzenlemeden önceki halleri, `shadow-` ve `passwd-` olarak ayrıca tutulur.
    - Eğer asıl dosyalara bir şey olursa, burdakiler kullanılabilir.
- `/etc/group`
    - Grupları ve içindeki kullanıcıları gösterir.
- `/etc/gpasswd`
    - Grupların parolarını tutar.
    - Genellikle gruplara parola verilmez. 
- `chown`
    - Dosya veya dizinin sahibi değiştirilebilinir.
    - `chown <yeni> <dizin>`
        - Sahipliğini değiştirir.
    - `chown <yeni>:<yeni> <dizin>`
        - Sahibini ve grubunu değiştirir.
    - `-R` parametresi kullanılarak alttaki dizin ve dosyaların sahipliği de değiştirilebilir.

#### GENEL

- Linux içinde nokta ile başlayan dosyalar veya dizinler gizli dosya olarak algılanır.
- Linux içinde herşey birer dosyadır.
- `/var/log`
    - Sistem loglarının tutulduğu kısımdır.
- `Alt + F1..F6` tuşlarıyla birden fazla terminal açılabilir.
- `~/.bashrc`
    - Bash başlatıldığında çalışacak komutları içerir.
    - Kalıcı alias tanımlamaları burda yapılabilir.
    - Her kullanıcının kendi home dizininde bulunur. Yoksa oluşturulabilir.
    - Değişiklik yapıldıktan sonra bash tekrar başlatılmalıdır.
        - `bash` komutu tekrar çalıştırılarak bash restart edilebilir.