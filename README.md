# 🐳 Docker Compose Monitoring Stack

Stack monitoring yang terdiri dari Node-RED, Grafana, Loki, Promtail, dan InfluxDB.

## 📋 Daftar Service

| Service | Image | Port | Status | Description |
|---------|-------|------|--------|-------------|
| Node-RED | `scada-stack-nodered` | 1880 | ✅ Healthy | Flow-based programming tool |
| Grafana | `grafana/grafana-oss:latest` | 3000 | ✅ Running | Visualization and analytics platform |
| Promtail | `grafana/promtail:latest` | - | ✅ Running | Log collection agent for Loki |
| Grafana Renderer | `grafana/grafana-image-renderer:latest` | 8081 | ✅ Healthy | Image rendering service for Grafana |
| Loki | `grafana/loki:latest` | 3100 | ✅ Running | Log aggregation system |
| InfluxDB | `influxdb:latest` | 8086 | ✅ Running | Time series database |

## ⚡ Quick Start

### 1. Build dan Jalankan Semua Service
```bash
docker compose up -d --build
```

### 2. Verifikasi Status Container
```bash
docker ps
```

### 3. Akses Aplikasi
- **Node-RED**: http://localhost:1880
- **Grafana**: http://localhost:3000
- **Loki API**: http://localhost:3100
- **InfluxDB**: http://localhost:8086

## 🔄 Update Stack

### Rebuild dan Restart
```bash
docker compose down
docker compose up -d --build
```

### Update Specific Service
```bash
docker compose build <service-name>
docker compose up -d <service-name>
```

## 📝 Monitoring dan Logs

### Lihat Log Real-time
```bash
docker compose logs -f
```

### Lihat Log Specific Service
```bash
docker compose logs -f nodered
docker compose logs -f grafana
docker compose logs -f loki
docker compose logs -f influxdb
```

### Cek Health Status
```bash
docker ps --format "table {{.Names}}\t{{.Status}}"
```

## ⚙️ Konfigurasi Default

### Port Configuration
- Node-RED: 1880
- Grafana: 3000  
- Grafana Renderer: 8081
- Loki: 3100
- InfluxDB: 8086

### Volume Locations
- Data persisten disimpan dalam Docker volumes
- Konfigurasi berada di direktori `config/` masing-masing service

## 🚨 Troubleshooting

### Service Tidak Berjalan
```bash
# Restart service yang bermasalah
docker compose restart <service-name>

# Lihat detail error
docker compose logs <service-name>
```

### Port Conflict
Jika port sudah digunakan, ubah port mapping di file `docker-compose.yml`

### Resource Issues
```bash
# Lihat resource usage
docker stats

# Clean up resources
docker system prune
```

### Permission Issues
```bash
# Fix volume permissions
sudo chown -R 1000:1000 ./data
```

## 📊 Health Check

Service dengan health check:
- ✅ Node-RED: Health check aktif
- ✅ Grafana Renderer: Health check aktif  
- ❌ Service lain: Monitoring via log inspection

## 🔧 Maintenance

### Backup Data
```bash
# Backup volumes
docker run --rm -v <volume-name>:/source -v $(pwd):/backup alpine tar czf /backup/backup.tar.gz -C /source .
```

### Update Images
```bash
# Pull images terbaru
docker compose pull

# Rebuild dengan images baru
docker compose up -d --build
```
---

**Note**: Dokumentasi ini untuk environment development. Untuk production, pertimbangkan konfigurasi keamanan tambahan dan environment variables.
