
# 📦 Setup Awal Server Ubuntu 22.04.5 (VM/VPS)

## 🎯 Tujuan
Mempersiapkan server Ubuntu 22.04.5 LTS agar aman, efisien, dan siap digunakan untuk kebutuhan web server, automation tools, DevOps workflow, atau production service lain. Fokus pada best practices saat provisioning awal server.

## 🖥️ Informasi Server
| Keterangan     | Detail              |
|----------------|---------------------|
| Hostname       | `student`  |
| OS             | Ubuntu 22.04.5 LTS  |
| IP Address     | `172.30.116.200`       |
| Akses awal     | via SSH (default port 22) |
| Akses baru     | via SSH port `2222` |

## ✅ Checklist Setup Awal
- [x] Update system packages
- [x] Tambah user baru non-root
- [x] Ubah port SSH & disable root login
- [x] Konfigurasi firewall UFW
- [x] Install web server (Nginx)

## 🔧 Langkah-Langkah Detail

### 🔹 1. Update Sistem
```bash
sudo apt update -y && sudo apt upgrade -y
```
> Tujuan: agar server memiliki versi paket terbaru dan aman.

### 🔹 2. Tambah User Baru (Non-root)
```bash
sudo adduser rifqi
sudo usermod -aG sudo rifqi
su - rifqi
groups
```
> Hindari login sebagai root langsung. Gunakan user sudo yang lebih aman.

### 🔹 3. Ubah Port SSH dan Nonaktifkan Root Login
```bash
sudo nano /etc/ssh/sshd_config
```
Ubah:
```ini
#Port 22
Port 2222

PermitRootLogin no
```
Restart SSH:
```bash
sudo systemctl restart sshd
```
Tes koneksi:
```bash
ssh rifqi@192.168.x.x -p 2222
```

### 🔹 4. Konfigurasi Firewall UFW
```bash
sudo ufw allow 2222/tcp
sudo ufw allow 80/tcp
sudo ufw enable
sudo ufw reload
sudo ufw status
```

### 🔹 5. Install Nginx
```bash
sudo apt install nginx -y
sudo systemctl status nginx
```
Cek:
```
http://192.168.x.x:80
```
