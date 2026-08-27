Remote Support Manager (RSM)

Remote Support Manager (RSM), RustDesk tabanlı uzaktan destek altyapısını tek bir Ubuntu sunucu üzerinden yönetmek için hazırlanmış web tabanlı bir yönetim katmanıdır.

RSM; RustDesk sunucusu, web yönetim paneli, istemci paket üretimi, oturum takibi ve temel sistem yönetimini tek yapıda birleştirir.

Güncel sürüm adayı: v1.0.0-rc2

Özellikler

Web tabanlı yönetim paneli
RustDesk hbbs ve hbbr Docker yönetimi
ID / Rendezvous Server yapılandırması
Relay Server yapılandırması
RustDesk public key yönetimi
Portable Windows istemci paketi oluşturma
Firma / ürün adı özelleştirme
Logo ve branding desteği
Public istemci indirme bağlantısı
Aktif relay oturumlarını izleme
Oturum sürelerini görüntüleme
Aktif oturum sonlandırma
Audit / sistem logları
Nginx reverse proxy
SQLite veritabanı
Systemd servisleri
Ubuntu 24.04 LTS desteği

Gereksinimler

Ubuntu Server 24.04 LTS
x86_64 işlemci
Minimum 2 CPU
Minimum 2 GB RAM
Minimum 20 GB disk
İnternet erişimi
Docker
Docker Compose
Python 3.12+
Nginx
SQLite

Hızlı Kurulum

tar -xzf remote-support-manager-v1.0.0-rc2.tar.gz
cd remote-support-manager-v1.0.0-rc2
sudo bash install.sh

Kurulum sonunda yönetim paneli adresi ve ilk admin parolası görüntülenir.

İlk giriş:

http://SERVER-IP/
Kullanıcı adı:
admin

FastAPI backend 127.0.0.1:8000 üzerinde çalışır ve doğrudan internete açılmamalıdır.

Portable İstemci

Üretilen paket örneği:

RemoteSupport.zip

İçerik:

RemoteSupport.exe
RustDesk2.toml
Baslat-ve-Yapilandir.cmd
README.txt
profile/

Servis Kontrolü

systemctl status rsm-panel.service
systemctl status rsm-rustdesk-sessions.service
systemctl status nginx
docker ps

Beklenen RustDesk konteynerleri:

rsm-hbbs
rsm-hbbr

Güvenlik

Public repository içerisinde aşağıdaki içerikler bulunmamalıdır:

rsm.db
secret.key
id_ed25519
*.bak
*.sqlite
generated client packages
customer configuration files
logs

RustDesk private key kesinlikle paylaşılmamalıdır.

Güncelleme

sudo bash update.sh

Kaldırma

sudo bash uninstall.sh

Sürüm

v1.0.0-rc2

Bu sürüm final v1.0.0 öncesi test amaçlı Release Candidate sürümüdür.
RustDesk

RSM, RustDesk altyapısını kullanır. RustDesk ayrı bir açık kaynak projedir ve kendi lisans koşullarına tabidir.
Bu proje RustDesk projesinin resmi ürünü değildir. ( Sorunluluk kabul edilemz )

Remote Support Manager — RSM
