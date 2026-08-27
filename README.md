[README.md](https://github.com/user-attachments/files/31504961/README.md)
# Remote Support Manager (RSM)

**Remote Support Manager (RSM)**, RustDesk tabanlı uzaktan destek altyapısını tek bir Ubuntu sunucu üzerinden yönetmek için hazırlanmış web tabanlı bir yönetim katmanıdır.

RSM; RustDesk sunucusu, web yönetim paneli, istemci paket üretimi, oturum takibi ve temel sistem yönetimini tek yapıda birleştirir.

> **Güncel sürüm adayı:** `v1.0.0-rc2`

---

## Özellikler

- Web tabanlı yönetim paneli
- RustDesk `hbbs` ve `hbbr` Docker yönetimi
- ID / Rendezvous Server yapılandırması
- Relay Server yapılandırması
- RustDesk public key yönetimi
- Portable Windows istemci paketi oluşturma
- Firma / ürün adı özelleştirme
- Logo ve branding desteği
- Public istemci indirme bağlantısı
- Aktif relay oturumlarını izleme
- Oturum sürelerini görüntüleme
- Aktif oturum sonlandırma
- Audit / sistem logları
- Nginx reverse proxy
- SQLite veritabanı
- systemd servisleri
- Ubuntu Server 24.04 LTS desteği

---

## Gereksinimler

- Ubuntu Server 24.04 LTS
- x86_64 işlemci
- Minimum 2 CPU
- Minimum 2 GB RAM
- Minimum 20 GB disk
- İnternet erişimi
- Docker
- Docker Compose
- Python 3.12+
- Nginx
- SQLite

---

## Hızlı Kurulum

Release paketini açın:

```bash
tar -xzf remote-support-manager-v1.0.0-rc2.tar.gz
cd remote-support-manager-v1.0.0-rc2
```

Kurulumu başlatın:

```bash
sudo bash install.sh
```

Kurulum tamamlandığında terminalde yönetim paneli adresi ve ilk `admin` parolası görüntülenir.

### İlk giriş

```text
http://SERVER-IP/
```

Kullanıcı adı:

```text
admin
```

> İlk admin parolasını kurulum sonunda kaydedin ve ilk girişten sonra değiştirin.

---

## RustDesk Portları

| Port | Protokol | Açıklama |
|---:|---|---|
| 21115 | TCP | RustDesk bağlantı servisi |
| 21116 | TCP | ID / Rendezvous |
| 21116 | UDP | Rendezvous / heartbeat |
| 21117 | TCP | Relay |
| 21118 | TCP | WebSocket |
| 21119 | TCP | Relay WebSocket |
| 80 | TCP | RSM Web Panel / HTTP |
| 443 | TCP | HTTPS kullanılıyorsa |
| 22 | TCP | SSH yönetimi |

Önerilen RustDesk firewall seti:

```text
TCP 21115-21119
UDP 21116
```

RSM FastAPI backend yalnızca:

```text
127.0.0.1:8000
```

üzerinde çalışmalı ve doğrudan internete açılmamalıdır.

---

## Portable İstemci Paketi

Üretilen paket örneği:

```text
RemoteSupport.zip
```

Paket içeriği:

```text
RemoteSupport.exe
RustDesk2.toml
Baslat-ve-Yapilandir.cmd
README.txt
profile/
```

---

## Servis Kontrolü

RSM Panel:

```bash
systemctl status rsm-panel.service
```

Session parser:

```bash
systemctl status rsm-rustdesk-sessions.service
```

Nginx:

```bash
systemctl status nginx
```

RustDesk:

```bash
docker ps
```

Beklenen konteynerler:

```text
rsm-hbbs
rsm-hbbr
```

---

## Güvenlik

Public repository içerisinde aşağıdaki dosyalar **bulunmamalıdır**:

```text
rsm.db
secret.key
id_ed25519
*.bak
*.sqlite
generated client packages
customer configuration files
logs
```

RustDesk private key olan `id_ed25519` kesinlikle paylaşılmamalıdır.

Yönetim panelinin mümkünse VPN, yönetim VLAN'ı veya güvenilir IP adresleri üzerinden erişilebilir olması önerilir.

---

## Güncelleme

```bash
sudo bash update.sh
```

Production sistemlerde güncelleme öncesi yedek alınması önerilir.

---

## Kaldırma

```bash
sudo bash uninstall.sh
```

---

## Sürüm Durumu

**Current release candidate:** `v1.0.0-rc2`

Bu sürüm final `v1.0.0` öncesinde kurulum ve gerçek ortam testleri için yayınlanmıştır.

---

## RustDesk

RSM, RustDesk altyapısını kullanır.

RustDesk ayrı bir açık kaynak projedir ve kendi lisans koşullarına tabidir.

**Remote Support Manager, RustDesk projesinin resmi ürünü değildir.**
*** SORUMLULUK KABUL EDİLMEZ ***

---

## Lisans

Lisans bilgileri için repository içerisindeki `LICENSE` ve varsa `NOTICE.md` dosyalarına bakın.

---

## Uyarı

Bu yazılım **Release Candidate** durumundadır.

Production ortamında kullanmadan önce:

- Firewall kurallarını kontrol edin
- Yedek alın
- İlk admin parolasını değiştirin
- RustDesk private key'i koruyun
- HTTPS yapılandırın
- Erişim politikalarını sınırlandırın
- Test bağlantısı gerçekleştirin

---

**Remote Support Manager — RSM**
