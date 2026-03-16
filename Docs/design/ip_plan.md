# TOPOLOGI PROYEK PBL MINGGU 3
Tabel berikut menunjukkan detail jaringan untuk skenario keamanan:

| Hostname               | Peran                    | Alamat IP     | Sistem Operasi        | Port Terbuka                  |
| ---------------------- | ------------------------ | ------------- | --------------------- | ----------------------------- |
| PC-Attacker-Node       | Penyerang / Penguji      | 192.168.5.25  | Kali Linux            | -                             |
| Target-Database-Server | Server database (Target) | 192.168.5.50  | Ubuntu Server (MySQL) | 3306 (Database), 22 (SSH)     |
| PC-Monitoring-Node     | IDS / Monitoring         | 192.168.5.75  | Security Onion        | 443 (HTTPS), 514 (TCP)        |

Detail port yang digunakan dalam skenario keamanan:

| Pelabuhan | Protokol | Layanan | Keterangan                                                            |
| --------- | -------- | ------- | --------------------------------------------------------------------- |
| 22        | TCP      | SSH     | Digunakan untuk remote administration dan simulasi brute force attack |
| 3306      | TCP      | MySQL   | Port layanan database pada server target                              |
| 514       | UDP      | Syslog  | Digunakan untuk mengirim log dari server target ke sistem monitoring  |
| 443       | TCP      | HTTPS   | Dashboard monitoring Security Onion                                   |