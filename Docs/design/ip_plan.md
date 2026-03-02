# TOPOLOGI PROYEK PBL MINGGU 3
Tabel berikut menunjukkan detail jaringan untuk skenario keamanan:

| Hostname                  | Peran               | Alamat IP         | Jaringan         | Sistem Operasi        | Port Terbuka    |
| ------------------------- | ------------------- | ----------------- | ---------------- | --------------------- | --------------- |
| PC-Attacker-Node          | Penyerang / Penguji | 192.168.5.5       | 192.168.5.0/24   | Kali Linux            | -               |
| Web-Server(DMZ)           | Server Target (DMZ) | 192.168.15.5      | 192.168.15.0/24  | Ubuntu Server / IIS   | 80/tcp, 443/tcp |
| Database-server(Internal) | Server Basis Data   | 192.168.25.5      | 192.168.25.0/24  | Ubuntu Server (MySQL) | 3306/tcp        |
| PC-Monitoring-Node        | IDS / Penjaga       | 192.168.35.5      | 192.168.35.0/24  | Security Onion        | Mode Monitoring |
| Router                    | Gerbang / Firewall  | Multi Interface   | Multi-Jaringan   | Cisco IOS             | Routing .md ACL   |
---



