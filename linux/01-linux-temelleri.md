# Linux Notlarım

Linux çalışırken öğrendiğim temel terminal komutlarını, dosya izinlerini ve süreç yönetimini burada topluyorum. Yeni şeyler öğrendikçe bu notları güncelleyeceğim.

---

## 1. Linux Terminal Komutları

### `pwd`

Terminalde şu anda hangi klasörde olduğumu gösterir.

```bash
pwd
```

Örnek çıktı:

```text
/home/aslan
```

Bu çıktı, şu anda `/home/aslan` klasöründe olduğumu gösterir.

`pwd` sistemde herhangi bir değişiklik yapmaz, sadece bulunduğum konumu gösterir.

---

### `ls`

Bulunduğum klasördeki dosya ve klasörlerin isimlerini listeler.

```bash
ls
```

Örnek çıktı:

```text
docs  notes  src  deneme.txt
```

Burada `docs`, `notes` ve `src` klasör, `deneme.txt` ise dosya olabilir.

Normal `ls` komutu gizli dosyaları ve ayrıntılı bilgileri göstermez.

---

### `ls -la`

Bulunduğum klasördeki dosya ve klasörleri gizli dosyalar dahil ayrıntılı şekilde gösterir.

```bash
ls -la
```

Örnek çıktı:

```text
-rw-rw-r-- 1 aslan aslan 749 Sep 5 19:26 terminal-komutlari.txt
```

Buradan dosyanın izinleri, sahibi, grubu, boyutu ve değiştirilme zamanı gibi bilgileri görebilirim.

---

### `cd`

Klasörler arasında geçiş yapmak için kullanılır.

```bash
cd klasor-adi
```

Bir üst klasöre çıkmak için:

```bash
cd ..
```

Örneğin bulunduğum yer:

```text
/home/aslan/can365-lab/ana
```

`cd ..` komutundan sonra:

```text
/home/aslan/can365-lab
```

konumuna geçmiş olurum.

---

### `mkdir`

Yeni klasör oluşturmak için kullanılır.

```bash
mkdir mkdir-egitimi
```

Komut başarılı olduğunda genellikle ekrana herhangi bir çıktı vermez.

#### `mkdir -p`

İç içe klasörleri tek komutla oluşturmak için kullanılabilir.

```bash
mkdir -p ana/alt
```

Burada `ana` klasörü yoksa önce onu, ardından `alt` klasörünü oluşturur.

`-p` kullanmadan:

```bash
mkdir ana/alt
```

komutunu çalıştırırsam ve `ana` klasörü yoksa hata alırım.

---

### `touch`

Dosya yoksa yeni ve boş bir dosya oluşturmak için kullanılabilir.

```bash
touch ilk-dosya.txt
```

Başarılı olduğunda genellikle çıktı vermez.

Başka bir klasörün içinde dosya oluşturmak için:

```bash
touch mkdir-egitimi/ana/alt/ilk-dosya.txt
```

Örnek klasör yapısı:

```text
mkdir-egitimi/
└── ana/
    └── alt/
        └── ilk-dosya.txt
```

---

### `cp`

Dosya kopyalamak için kullanılır.

Genel kullanım:

```bash
cp kaynak-dosya hedef-dosya
```

Örnek:

```bash
cp not.txt not-kopya.txt
```

Burada `not.txt` kaynak dosya, `not-kopya.txt` ise oluşturulacak kopyadır.

---

### `mv`

Dosyayı taşımak veya yeniden adlandırmak için kullanılır.

Dosya adını değiştirmek:

```bash
mv eski-ad.txt yeni-ad.txt
```

Dosyayı başka klasöre taşımak:

```bash
mv yeni-ad.txt notes/
```

Aynı klasörde farklı bir isim verirsem dosyanın adı değişir. Başka bir klasörü hedef gösterirsem dosya taşınır.

---

### `rm`

Dosya silmek için kullanılır.

```bash
rm dosya-adi
```

Örnek:

```bash
rm deneme.txt
```

`rm` ile sildiğim dosya normalde çöp kutusuna gitmez. Bu yüzden çalıştırmadan önce dosya adını ve bulunduğum konumu kontrol etmem gerekir.

---

### `find`

Dosya veya klasör aramak için kullanılır.

Genel kullanım:

```bash
find aranacak-konum -name "aranacak-ad"
```

Örnek:

```bash
find . -name "deneme.txt"
```

Buradaki `.` aramanın bulunduğum klasörden başlamasını sağlar.

`-name` ise dosyayı adına göre arar.

---

# 2. Linux Dosya İzinleri

### `ls -l`

Dosya veya klasörlerin izinlerini, sahibini, grubunu, boyutunu ve değiştirilme tarihini görmek için kullanılır.

```bash
ls -l izin-deneme.txt
```

Örnek çıktı:

```text
-rw-r----- 1 aslan aslan 0 Sep 5 19:45 izin-deneme.txt
```

Burada:

* `-rw-r-----` → dosyanın izinleri
* `1` → bağlantı sayısı
* İlk `aslan` → dosyanın sahibi
* İkinci `aslan` → dosyanın ait olduğu grup
* `0` → dosyanın byte cinsinden boyutu
* `Sep 5 19:45` → son değiştirilme zamanı
* `izin-deneme.txt` → dosyanın adı

---

### `chmod`

Dosya veya klasör izinlerini değiştirmek için kullanılır.

```bash
chmod 640 izin-deneme.txt
```

Örnek izin görünümü:

```text
-rw-r-----
```

Linux'ta temel izinların sayısal değerleri:

```text
r = read    = okuma       = 4
w = write   = yazma       = 2
x = execute = çalıştırma  = 1
```

Hepsi birlikte:

```text
rwx = 4 + 2 + 1 = 7
```

Linux izinlerinde kullanılan üç rakam sırasıyla:

```text
1. rakam = dosya sahibi
2. rakam = grup
3. rakam = diğer kullanıcılar
```

Örneğin:

```bash
chmod 640 izin-deneme.txt
```

Burada:

```text
6 = rw- = sahibi okuyabilir ve yazabilir
4 = r-- = grup sadece okuyabilir
0 = --- = diğer kullanıcıların izni yok
```

### Sayısal izin tablosu

```text
0 = --- = hiçbir izin yok
1 = --x = çalıştırma
2 = -w- = yazma
3 = -wx = yazma + çalıştırma
4 = r-- = okuma
5 = r-x = okuma + çalıştırma
6 = rw- = okuma + yazma
7 = rwx = okuma + yazma + çalıştırma
```

Bir metin dosyasına `x` izni vermek onu otomatik olarak bir programa dönüştürmez. Dosyanın içinde çalıştırılabilir bir içerik olması gerekir.

---

# 3. Linux Süreç Yönetimi

### `ps`

Mevcut terminal oturumuyla ilişkili çalışan süreçleri gösterir.

```bash
ps
```

Örnek çıktı:

```text
PID     TTY      TIME       CMD
5397    pts/0    00:00:00   bash
```

Burada:

* `PID` → sürecin numarası
* `TTY` → sürecin bağlı olduğu terminal
* `TIME` → sürecin kullandığı CPU süresi
* `CMD` → çalışan komut veya program

---

### `pgrep`

Bir süreci adına göre arayıp PID numarasını görmek için kullanılır.

```bash
pgrep sleep
```

Örnek çıktı:

```text
12845
```

Buradaki `12845`, çalışan `sleep` sürecinin PID numarasıdır.

---

### `top`

Sistemde çalışan süreçleri ve CPU/RAM kullanımını canlı olarak gösterir.

```bash
top
```

Burada özellikle baktığım alanlar:

* `Tasks` → süreçlerin genel durumu
* `%CPU` → CPU kullanımı
* `%MEM` → RAM kullanımı
* `PID` → süreç numarası
* `USER` → süreci çalıştıran kullanıcı
* `COMMAND` → çalışan komut veya program

`top` ekranından çıkmak için `q` tuşuna basabilirim.

---

## PID Nedir?

PID, **Process ID** anlamına gelir.

Linux çalışan her sürece bir PID numarası verir.

Örnek:

```text
12845
```

Bu numara çalışan bir `sleep` sürecine ait olabilir.

PID üzerinden bir süreci kontrol edebilir, durdurabilir, devam ettirebilir veya kapatabilirim.

Süreç kapandıktan sonra o sürece ait PID artık geçerli olmaz.

---

### `kill`

PID numarasını bildiğim bir sürece sinyal göndermek için kullanılır.

```bash
kill PID
```

Örnek:

```bash
kill 12845
```

Normal `kill` komutu varsayılan olarak `SIGTERM` sinyali gönderir.

Bu sinyal sürece düzgün şekilde kapanmasını söyler.

Süreç kapandı mı diye kontrol etmek için:

```bash
pgrep sleep
```

kullanabilirim.

Çıktı gelmiyorsa süreç artık çalışmıyordur.

---

# 4. Linux Sinyalleri

## SIGTERM

Normal kapanma sinyalidir.

Sinyal numarası:

```text
15
```

Kullanımı:

```bash
kill PID
```

Örnek:

```bash
kill 13527
```

Mümkün olduğunda süreçleri önce bu şekilde kapatmak daha doğru.

---

## SIGSTOP

Bir süreci tamamen kapatmadan geçici olarak durdurmak için kullanılır.

```bash
kill -STOP PID
```

Örnek:

```bash
kill -STOP 13527
```

Süreç bellekte kalır ama çalışması durur.

---

## SIGCONT

Durdurulmuş bir süreci tekrar devam ettirmek için kullanılır.

```bash
kill -CONT PID
```

Örnek:

```bash
kill -CONT 13527
```

---

## SIGKILL

Süreci zorla kapatmak için kullanılır.

Sinyal numarası:

```text
9
```

Kullanımı:

```bash
kill -9 PID
```

Örnek:

```bash
kill -9 13527
```

Bunu normal `kill` işe yaramadığında son çare olarak kullanmak gerekir.

Çünkü `SIGKILL` sürece düzgün kapanması için fırsat vermez.

---

# 5. Yaptığım Süreç Yönetimi Uygulaması

Önce test için bir süreç başlattım:

```bash
sleep 300 &
```

PID numarasını buldum:

```bash
pgrep sleep
```

Süreci geçici olarak durdurdum:

```bash
kill -STOP PID
```

Durumunu kontrol ettim:

```bash
ps -o pid,stat,cmd -p PID
```

Tekrar devam ettirdim:

```bash
kill -CONT PID
```

Sonra normal şekilde kapattım:

```bash
kill PID
```

Son olarak çalışıp çalışmadığını kontrol ettim:

```bash
pgrep sleep
```

Çıktı gelmezse süreç kapanmış demektir.

---

# Kısa Özet

```text
pwd          → Bulunduğum klasörü gösterir.
ls           → Dosya ve klasörleri listeler.
ls -la       → Gizli dosyalar dahil ayrıntılı liste gösterir.
cd           → Klasör değiştirir.
mkdir        → Yeni klasör oluşturur.
mkdir -p     → İç içe klasörleri oluşturur.
touch        → Dosya oluşturmak için kullanılabilir.
cp           → Dosya kopyalar.
mv           → Dosya taşır veya yeniden adlandırır.
rm           → Dosya siler.
find         → Dosya veya klasör arar.

ls -l        → Dosya izinlerini gösterir.
chmod        → Dosya izinlerini değiştirir.

ps           → Terminaldeki süreçleri gösterir.
pgrep        → Süreci adına göre bulur.
top          → Süreçleri canlı olarak gösterir.
kill PID     → Sürece normal kapanma sinyali gönderir.
kill -STOP   → Süreci geçici olarak durdurur.
kill -CONT   → Süreci devam ettirir.
kill -9      → Süreci zorla kapatır.
```

## Şu ana kadar öğrendiklerim

Bu çalışmalarla beraber Linux'ta temel olarak:

* terminalde klasörler arasında hareket etmeyi,
* dosya ve klasör oluşturmayı,
* dosyaları kopyalamayı, taşımayı ve silmeyi,
* dosya aramayı,
* Linux dosya izinlerinin mantığını,
* `chmod` ile izin değiştirmeyi,
* çalışan süreçleri görüntülemeyi,
* PID mantığını,
* süreçleri durdurmayı ve devam ettirmeyi,
* süreçleri normal veya zorla kapatmayı

öğrendim.

Bu dosyayı Linux öğrendikçe güncellemeye devam edeceğim.
