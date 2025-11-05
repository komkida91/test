# 🍓 Backup Configuración Raspberry Pi

Este directorio contiene backups automáticos de la configuración de la Raspberry Pi.

---

## 📋 ¿Qué contiene el backup?

- ✅ Configuración completa de Nginx
- ✅ Certificados SSL (Let's Encrypt)
- ✅ Servicios systemd
- ✅ Configuración de red
- ✅ Scripts DuckDNS
- ✅ Cron jobs
- ✅ Información del sistema y paquetes instalados

---

## 🔄 Frecuencia de Backup

- **Automático:** Cada día a las 3 AM UTC
- **Manual:** Se puede ejecutar desde GitHub Actions

---

## 📦 Archivos de Backup

Los backups se guardan como archivos `.tar.gz` con el formato:
```
raspberry-backup-YYYYMMDD-HHMMSS.tar.gz
```

**Último backup:** `raspberry-backup-latest.tar.gz`

---

## 🔧 Restaurar desde Backup

Ver la documentación completa en:
[`repo-automation/docs/RASPBERRY-BACKUP.md`](../../repo-automation/docs/RASPBERRY-BACKUP.md)

### Resumen Rápido:

1. **Instalar sistema base** (Raspberry Pi OS)
2. **Instalar paquetes esenciales:**
   ```bash
   sudo apt-get update && sudo apt-get upgrade -y
   sudo apt-get install -y nginx certbot python3-certbot-nginx openssh-server
   ```
3. **Descargar y extraer backup:**
   ```bash
   git clone https://github.com/komkida91/test.git
   cd test/raspberry-backup
   tar -xzf raspberry-backup-latest.tar.gz
   ```
4. **Restaurar configuración:**
   ```bash
   sudo cp -r nginx/* /etc/nginx/
   sudo cp -r letsencrypt/* /etc/letsencrypt/  # Si existe
   sudo cp -r systemd/* /etc/systemd/system/
   sudo cp dhcpcd.conf /etc/dhcpcd.conf
   sudo cp hosts /etc/hosts
   crontab crontab.txt
   ```
5. **Verificar y reiniciar:**
   ```bash
   sudo nginx -t
   sudo systemctl daemon-reload
   sudo systemctl restart nginx
   ```

---

## ⚠️ Notas Importantes

- **Certificados SSL:** Pueden regenerarse con `sudo certbot renew --nginx`
- **Secrets:** Los secrets de GitHub NO se incluyen en el backup (por seguridad)
- **IP Dinámica:** Si la IP cambia, actualizar DuckDNS manualmente

---

**Última actualización:** 2025-11-04

