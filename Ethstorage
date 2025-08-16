# EthStorage V1 Trusted Setup — Ubuntu 22.04 (Screen ile)

> Bu repo taslağı, VPS üzerinde EthStorage V1 Trusted Setup törenine katılmak için **adım adım** komutları içerir.

> Kopyala yapıştır ile çalışır. Terminalde `screen` veya `tmux` kullanabilirsin, aşağıda **screen** akışı verilmiştir.

---

## İçindekiler

- [Önkoşullar](#önkoşullar)
- [Hızlı Kurulum](#hızlı-kurulum)
- [GitHub Yetkilendirme](#github-yetkilendirme)
- [Katılım (Screen ile)](#katılım-screen-ile)
- [Temizlik](#temizlik)
- [Sorun Giderme](#sorun-giderme)
- [SSS](#sss)

---

## Önkoşullar

- **VPS**: Ubuntu 22.04 LTS
- **Node.js**: v18.x (NVM ile kuracağız)
- **npm**: 9.2+ (Node 18 ile uygundur)
- **GitHub hesabı**: Blogdaki şartlara uygun (hesap yaşı en az 1 aylık, en az 1 repo, en az 1 takipçi ve en az 5 kişi takip)
- **Stabil bağlantı**: Özellikle upload hızın düşük olmasın
- **Gereksinimler yüksek değil, 2Gb Ram Vps ile halledersin**

> **Resmî kaynak:** EthStorage blogundaki “Join the EthStorage V1 Trusted Setup Ceremony” yazısı.

---

## Hızlı Kurulum

### 1) Sistem güncelle ve araçları kur
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git build-essential screen htop
```

### 2) NVM ile Node.js 18 kur
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install 18
nvm use 18
npm -v || npm install -g npm@latest
```

### 3) Çalışma klasörü
```bash
mkdir -p ~/trusted-setup-tmp && cd ~/trusted-setup-tmp
```

### 4) CLI kur
```bash
npm install -g @p0tion/phase2cli
```

## GitHub Yetkilendirme

```bash
phase2cli auth

```
- Komut sana bir device code ve URL verecek.
- Tarayıcıdan URL’yi aç → GitHub ile giriş yap → yetkilendir. https://github.com/login/device
- Terminalde “Congratulations, you're all set!” görmelisin.

## Katılım (Screen ile)

### Yeni bir screen oturumu başlat
```bash
screen -S ceremony
```
## Törene katıl
```bash
phase2cli contribute -c ethstorage-v1-trusted-setup-ceremony
```
👉 İpucu: “entropy” sorarsa Enter ile "Random" seçerek otomatik üretimi kabul edebilirsin.

- Screen'den ayrıl (arka planda çalışsın): Ctrl + A, sonra D
- Geri dönmek için: screen -r ceremony
- Sıraya gireceksin ve önünde kaç kişi olduğunu, bekleme süreni göreceksin ama bu stabil olmayabilir
- Sabırla sıranın gelmesini beklemen lazım, takip etmen lazım, sıra sana gelince onay vermen lazım.

## Sana yardımcı olacak kodlar

`<screen isim>` kısmını silip, oraya sizin screen isminizi yazmanız gerekir

```bash
screen yüklü değilse
apt-get install screen

yeni screen ekranı açmak için
screen -S <screen isim>

aktif olan screenleri görmek için
screen -ls

aktif screen ekranına detached iken girmek için
screen -r <screen isim>

aktif screen ekranına attached (düzgün çıkmadıysanız) iken girmek için
screen -d -r <screen isim>

aktif bir screen ekranını tamamen kapatmak için
screen -S <screen isim> -X quit 

```
# Temizlik

### İş bittikten sonra bu kodlar ile temizleyin
```bash
phase2cli clean
phase2cli logout
cd ~ && rm -rf ~/trusted-setup-tmp
```

## Sorun Giderme
### 1) DNS çözülmüyor (Name or service not known)

### systemd-resolved reset
```bash
sudo systemctl restart systemd-resolved
sudo resolvectl flush-caches
```

### Gerekirse kalıcı nameserver
```bash
echo -e "nameserver 8.8.8.8\nnameserver 1.1.1.1" | sudo tee /etc/resolv.conf

ping -c 3 google.com
```

### 2) Koordinatöre bağlantı testi
```bash
sudo apt install -y netcat-traditional
nc -vz ceremony.ethstorage.net 443
```
Başarılı örnek: succeeded!

## 3) Kuyruk takılı kaldı (contributors sayısı değişmiyor)

### Çık ve tekrar başlat
Ctrl + C ile screen içinde durdur ve tekrar başlat
```bash
phase2cli contribute -c ethstorage-v1-trusted-setup-ceremony
```

## 4) Kaynaklar yetmiyor

- Küçük devreler için 2 GB RAM yeterlidir.
- Büyük devrelerde 4-8 GB+ önerilir.
- `htop` komutu ile CPU/RAM’i izle, katkı sırasında CPU yükselmelidir.

# SSS

**S: Screen yerine tmux kullanabilir miyim?**
C: Evet. `tmux new -s ceremony` ile oturum aç, ayrılmak için `Ctrl+B, D`.

**S: Repo/klasör silersem GitHub yetkim gider mi?**
C: Hayır. `phase2cli logout` yapmadıkça token durur, en kötü yeniden `auth` istenir.

**S: Komutu nerede çalıştırmalıyım?**
C: `~/trusted-setup-tmp` gibi izole bir klasörde.

**S: Katkı sırasında sıra takıldı, ilerlemiyor. Ne yapmalıyım?**
C: Takılırsa → Ctrl + C ile durdur → tekrar şu komutu çalıştır:
`phase2cli contribute -c ethstorage-v1-trusted-setup-ceremony`

**⏳ Kuyrukta uzun süre ilerleme olmaması → normal olabilir, sabır gerekebilir.**
