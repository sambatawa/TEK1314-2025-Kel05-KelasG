# Proyek PBL Keamanan Siber - Kelompok 5 kelas G

## Anggota Kelompok

1. Inas Samara Taqia – Lead Analyst
2. Irfan Rifqy Widya Syahbani – System/Network Engineer
3. Ariel Pasha Ramaditya – Security Analyst 1
4. Daffa Ardyana Eka Putra – Security Analyst 2

## Deskripsi Skenario

Pada proyek Internal Database Fortress, kami merancang dan membangun sebuah sistem keamanan untuk melindungi server database internal yang berfungsi sebagai penyimpanan data penting organisasi. Infrastruktur terdiri dari tiga node utama, yaitu Attacker Node (Kali Linux), Target Database Server (Ubuntu Server dengan MySQL), dan Monitoring Node (Security Onion). Server database dijalankan pada Ubuntu Server dengan layanan MySQL (port 3306) serta akses administrasi melalui SSH (port 22). Karena sifatnya sebagai sistem internal, server ini menjadi target dari ancaman internal (insider threat) maupun pihak yang berhasil mengakses jaringan.

Untuk mensimulasikan ancaman tersebut, digunakan Attacker Node (Kali Linux) yang melakukan aktivitas ICMP Ping (reconnaissance), Network scanning, Simulasi brute force terhadap layanan SSH. Seluruh aktivitas jaringan dimonitor menggunakan Security Onion yang berfungsi sebagai sistem Intrusion Detection System (IDS) untuk merekam dan memonitor seluruh aktivitas jaringan yang mendeteksi potensi ancaman terhadap database server. Fokus pada fase ini adalah melakukan hardening terhadap server database dan memastikan bahwa seluruh aktivitas mencurigakan dapat terdeteksi oleh sistem monitoring sebelum memasuki fase serangan.

Tujuan utama dari proyek ini adalah:
* Membangun dan mengamankan sistem database internal melalui penerapan system hardening dan pengamanan akses layanan (MySQL dan SSH)
* Mendeteksi aktivitas mencurigakan berupa reconnaissance (ping, scanning) dan percobaan serangan
* Memonitor dan menganalisis traffic jaringan menggunakan Security Onion sebagai baseline sebelum simulasi serangan lanjutan

## Topologi Jaringan

Topologi jaringan yang digunakan adalah topologi sederhana berbasis satu segmen jaringan internal:

| Hostname               | Peran                    | Alamat IP    | Sistem Operasi        | Port Terbuka              |
| ---------------------- | ------------------------ | ------------ | --------------------- | ------------------------- |
| PC-Attacker-Node       | Penyerang / Penguji      | 192.168.5.25 | Kali Linux            | -                         |
| Target-Database-Server | Server database (Target) | 192.168.5.50 | Ubuntu Server (MySQL) | 3306 (Database), 22 (SSH) |
| PC-Monitoring-Node     | IDS / Monitoring         | 192.168.5.75 | Security Onion        | 443 (HTTPS), 514 (TCP)    |
Semua perangkat berada dalam satu subnet 192.168.5.0/24

## Detail Port dan Layanan

| Port | Protokol | Layanan | Keterangan                             |
| ---- | -------- | ------- | -------------------------------------- |
| 22   | TCP      | SSH     | Remote access dan simulasi brute force |
| 3306 | TCP      | MySQL   | Layanan database utama                 |
| 514  | UDP      | Syslog  | Pengiriman log ke monitoring           |
| 443  | TCP      | HTTPS   | Akses dashboard Security Onion         |

