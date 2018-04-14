#### Komutlar

- `cp`
    - Kopyalama yapar.
    - Dizin kopyalanacaksa ve içinde dosya varsa `-R` parametresi eklenmesi gereklidir.
- `mv`
    - Taşıma yapar.
    - Dizin kopyalarken herhangi bir şey yapmaya gerek yoktur.
- `wc <dosya>`
    - `word count`
    - Dosya içeriğini sayar.
    - Sonuç olarak (satır - kelime - harf) bilgisini verir.
- `cd`
    - Change Directory
    - Dizin değiştirme
    - Son iki değişim arasında geçiş yapmak için `cd -` kullanılabilir.
    - Tek başına kullanıldığında home dizinine gider.
- `which <komut>`
    - Komutun nerde olduğu bilgisini verir.
- `file <dosya>`
    - Dosyanın türü hakkında bilgi verir.
- `echo <yazı>`
    - Yazılan yazıyı ekrana basar
    - `echo <yazi> >> <dosya>`
        - Dosyaya herhangi bir ekleme yapmayı sağlar.

#### Linkler

- Hard link
    - Aynı disk üzerinde olmalıdır.
    - Dosyanın birebir aynısı oluşur.
- Soft Link
    - Herhangi bir yerde olabilir.
    - Yeni bir dosya oluşur, dosya içerik olarak sadece link verdiği adres barındırır.

#### Output yönlendirme

- 3 tane I/O birimi vardır:
    - `stdin` - `0`
        - İnput alınan kısımdır.
        - Varsayılan olarak klavyedir.
    - `stdout` - `1`
        - Output verilen kısımdır.
        - Varsayılan olarak konsoldur.
    - `stderr` - `2`
        - Standart olarak hata basılan kısımdır.
        - Varsayılan olarak konsoldur.
- `<komut> 1> sonuc.txt 2> hata.txt`
    - Burada çıktı (1) sonuc.txt dosyasına,
    - Hatalar (2) hata.txt dosyasına aktarılır.
- `<komut> &> sonuc.txt`
    - Hem çıktı hem de error birlikte sonuç.txt dosyasına aktarılır.
- `<komut> 1> /dev/null`
    - Buradaki tüm input çıktıları null dosyasına aktarılarak, aslında kaybediliyor.
    - Çünkü burdaki null bir cihaz gibi davranır ve gelen her şeyi kaybeder.
- `<komut> < <dosya>`
    - Sağdaki dosyayı veya komutu input gibi soldaki kısma aktarır.
    - Buradaki `<` işareti `0` kanalına yönlendirme yapar.
- `cat > cikti.txt`
    - `cat` komutu normalde 0 dan aldığını 1 e yönlendirir.
    - Biz bunun 1 çıktısını dosya olarak atarsak, yazdıklarımızı direk dosya içine yazabiliriz.
- Çıktılarda `>` kullanılırsa overwrite yapar, `>>` append yapar.
- `>` veya `>>` tek başına kullanılırsa default olarak 1 kanalını yönlendirme yapar.
- **NOT!** : `>` veya `>>` sadece dosyaya gönderme yapar, başka bir komuta gönderme yapamaz.
    - Bunun için aşağıdaki kımsı kullanabiliriz.

#### Programların çıktılarını yönlendirme

- Bunun için pipe `|` kullanılır.
- `<komut> | <komut>`
    - Sol taraftaki komutun çıktısı sağ tarafa input olarak verilir.

#### Değişken tanımlama

- `degisken=value`
    - Değişken ataması
- `echoe $degisken`
    - Değişken yazdırma
- Tanımlarken normal, kullanırken başında $ işaretiyle kullanıyoruz.

#### Linux IP alma

- `dhclient`
    - IP atanmasını sağlar.
    - Session süresince geçerlidir. 
    - `dhclient -r`
        - Bu komutla aktif olan ip bırakılabilir.
- `ip a`
    - IP adresi ve diğer bilgilere ulaşılabilir.

#### Paket yöneticisi

- CentOS sistemleri için default `rpm` gelmektedir.
- rpm paket bağımlılıklarını, güncellemeleri, upgrade işlemlerini yönetemediği için genellikle `yum` kullanırız.
- Paket yöneticisi (yum) güncelleme, upgrade etme vs gibi işlemleri yapmaktadır.
- **NOT:** yum, rpm'i kullanır.
- `yum install <pack_name>`
    - **Paket ismini** veya **`.rpm`** dosyasını vererek kurulum yapmayı sağlar.
- `yum list installed`
    - Yüklü uygulamaları gösterir.
- `yum remove <pack>`
    - Yüklü uygulamayı kaldırır.
- `yum info <pack>`
    - Paket hakkında bilgi getirir.
- `yum install --downloadonly --downloaddir=<path> <pack>`
    - Paketin `.rpm` dosyasını verdiğimiz path'e indirir.
- `rpm -i <dosya.rpm>` 
    - rpm dosyasını kurmaya yarar.
- `rpm -e <pack>`
    - rpm paketini siler.
- `rpm -ql <pack>`
    - Paketin tüm dosyalarının nerde olduğunu gösterir.
- `rpm -qc <pack>`
    - Paketin tüm ayarlarının nerde olduğunu gösterir.
- `yum grouplist`
    - Belirli amaçlara göre paketlerin grup altına toplanmış ve toptan indirilmesine izin verilmiş hallerini burdan görebiliriz.
- `yum groupinstall "<group name>"`
    - Grupların indirilmesini sağlar.
- `yum repolist`
    - Açık olan ve paketlerin çekildiği repo adreslerini gösterir.
- `yum install epel-release`
    - yum'un default gelen repolarında bulunmayan çoğu paket, bu repo içinde bulunur. 
    - Yukarıdaki komut ile bunu repolara ekleyebiliriz.
- `yum search <string>`
    - Verilen string ile ilgili arama yapmaya yarar.
- `/etc/yum.repos.d`
    - Bu dizinde repoların bilgileri bulunur.
    - Herhangi bir repo dosyası içine girilip `enabled` kısmı değiştirilerek aktifleştirme ve deaktifleştime işlemleri yapılabilir.
- `yum history`
    - Daha önce yapılmış işlemleri gösterir.
    - `yum history info <sira_no>`
        - Bu komut ile, listedeki herhangi bir işlemin ayrıntıları görülebilir.
    - `yum history undo <sira_no>`
        - Yapılan bir işlemi geri almaya yarar.
    - `yum history redo <sira_no>`
        - Yapılan bir işlemi ileri almaya yarar.

#### Genel Notlar

- Root kullanıcılarında (#) diğer kullanıcılarda ($) işareti vardır.
- `id` parametresi kullanılarak kullanıcı ile ilgili ayrıntılara ulaşılabilir.
- `Ctrl + D` komutu `exit` komutu yerine geçer.
- `<komut> | less`
    - Genel olarak komutların sonuçlarını daha efektif şekilde görüntelemeyi sağlar.
- `lynx` > paket
    - Konsol üzerinde web tarayıcı kullanmaya yarar.