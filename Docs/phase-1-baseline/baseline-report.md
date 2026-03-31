# Baseline Report

## Topologi Jaringan

Topologi jaringan yang digunakan pada fase *baseline* adalah topologi sederhana satu segmen internal yang terdiri dari tiga *node* utama. Semua *host* berada di *subnet* `192.168.5.0/24` untuk memudahkan *monitoring* dan isolasi terhadap trafik internal.

| Hostname | Peran | Alamat IP | Sistem Operasi |
| :--- | :--- | :--- | :--- |
| **ATT-KEL05** | Penyerang / Penguji | `192.168.5.25` | labVM Linux (CyberOps) |
| **SRV-DB-KEL05** | Server Database (Target) | `192.168.5.50` | Ubuntu Server (24.04.3) |
| **MTR-KEL05** | IDS / Monitoring | `192.168.5.75` | Security Onion (2.4.211) |

## 1. Konfigurasi Jaringan

* Subnet internal menggunakan `192.168.5.0/24`.
* *Gateway* tidak diperlukan jika semua *node* berada dalam satu jaringan virtual yang sama, tetapi dapat dikonfigurasi sebagai rute *default* pada `192.168.5.1` jika diperlukan.
* *Firewall* internal hanya mengizinkan akses yang diperlukan ke beberapa layanan spesifik, yaitu port **3306** (MySQL) dan **22** (SSH).

## 2. Konfigurasi Layanan dan Port

* **SRV-DB-KEL05**
    * **SSH (Port 22):** Digunakan untuk pembatasan akses remote/administrasi.
    * **MySQL (Port 3306):** Sebagai database internal target yang diuji; akses dibatasi hanya dari subnet internal.
* **MTR-KEL05**
    * **Security Onion:** Menjalankan sensor IDS untuk memantau trafik jaringan.
    * **Dashboard HTTPS (Port 443):** Digunakan untuk akses antarmuka web Security Onion.

## 3. Hardening Server Database (SRV-DB-KEL05)

* Melakukan *update* dan *upgrade* sistem operasi serta paket lainnya menggunakan perintah `sudo apt update` dan `sudo apt upgrade`.
* Konfigurasi *firewall* melalui UFW (*Uncomplicated Firewall*) dengan aturan berikut:
    * `sudo ufw default deny incoming` (menutup koneksi masuk secara *default*).
    * `sudo ufw default allow outgoing` (membuka koneksi keluar secara *default*).
    * `sudo ufw allow 22/tcp` (membuka port 22 untuk SSH).
    * `sudo ufw allow 3306/tcp` (membuka port 3306 untuk MySQL).
* Pada file konfigurasi `sshd_config` di direktori `/etc/ssh`, parameter diubah menjadi `PermitRootLogin no` dan `PasswordAuthentication yes`.
* Pembatasan koneksi MySQL diatur pada parameter `bind-address` ke IP `192.168.5.50`.
* Pembuatan akun MySQL dibatasi hanya dengan hak akses ke aplikasi dan administrasi. Diterapkan juga penggunaan *password* yang kuat dan pengauditan log akses.

## 4. Konfigurasi Monitoring dan IDS (MTR-KEL05)

* Memastikan Security Onion untuk *monitor* trafik jaringan dan sistem berjalan normal (dapat dicek dengan perintah `so-status`).
* Pengaktifan sensor IDS Suricata untuk mendeteksi aktivitas *reconnaissance*, *port scan*.
* Menyiapkan *dashboard* dan *alert* dasar untuk memantau:
    * Kegiatan ICMP ping dan *network scanning*.
    * Akses tidak sah ke layanan MySQL.

## 5. Bukti Logging

Di labVM attacker:
* `ping 192.168.5.50`

Hasil yang muncul di security onion
* `sudo tcpdump -i eth1`
output:
* Timestamp
* Source IP: `192.168.5.25`
* Destination IP: `192.168.5.50`
* Protocol: `ICMP`
