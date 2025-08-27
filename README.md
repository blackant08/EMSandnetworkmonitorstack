# 🚀 Deployment dengan Docker Compose

Panduan singkat untuk build & menjalankan aplikasi menggunakan **Docker Compose**.

---

## ⚡ Pertama Kali Install

1. **Build image**
   ```bash
   docker compose build

    Jalankan container

docker compose up -d

Cek container

    docker ps

    Pastikan semua service running tanpa error.

🔄 Update Aplikasi

    Rebuild image

docker compose build

Restart container

docker compose down && docker compose up -d

Verifikasi container

    docker ps

    Pastikan service sudah jalan dengan image terbaru.

📝 Catatan

    Gunakan docker compose logs -f untuk melihat log service secara realtime.

    Jika hanya ingin rebuild + langsung jalanin, bisa pakai shortcut:

docker compose up -d --build
