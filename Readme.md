Deskripsi Skenario

Pada proyek ini, kami menggunakan skenario Internal Database Fortress, yaitu konsep jaringan di mana data penting (database) disimpan di jaringan internal yang lebih aman dan tidak bisa diakses langsung dari luar.

Web server ditempatkan di area DMZ supaya tetap bisa diakses oleh attacker untuk keperluan simulasi serangan. Jadi, attacker hanya bisa berinteraksi dengan web server terlebih dahulu, tidak langsung ke database.

Jika ingin mengakses database, harus melalui web server sebagai perantara. Selain itu, router digunakan sebagai gateway sekaligus firewall (menggunakan ACL) untuk mengatur dan membatasi akses antar jaringan. Seluruh aktivitas jaringan juga dimonitor menggunakan sistem IDS untuk mendeteksi jika ada aktivitas mencurigakan.