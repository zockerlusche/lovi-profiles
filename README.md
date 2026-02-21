# LoVi Profiles

App-Profile für [LoVi – Log Viewer](https://github.com/zockerlusche/lovi).

Ein Profil definiert wie LoVi die Log-Levels einer App erkennt und zeigt dir den genauen docker-compose Mount den du brauchst.

---

## Verfügbare Profile

| App | Kategorie | Version | Log-Pfad |
|-----|-----------|---------|----------|
| Radarr | ARR | 1.0 | `/opt/docker/logs/radarr/` |
| Sonarr | ARR | 1.0 | `/opt/docker/logs/sonarr/` |
| Lidarr | ARR | 1.0 | `/opt/docker/logs/lidarr/` |
| Readarr | ARR | 1.0 | `/opt/docker/logs/readarr/` |
| Prowlarr | ARR | 1.0 | `/opt/docker/logs/prowlarr/` |
| Whisparr | ARR | 1.0 | `/opt/docker/logs/whisparr/` |
| SABnzbd | Download | 1.0 | `/opt/docker/logs/sabnzbd/` |
| Jellyfin | Media | 1.0 | `/opt/docker/logs/jellyfin/` |
| Nginx | Network | 1.0 | `/opt/docker/logs/nginx/` |
| Traefik | Network | 1.0 | `/opt/docker/logs/traefik/` |
| Home Assistant | Automation | 1.0 | `/opt/docker/logs/homeassistant/` |
| Syslog | System | 1.0 | `/opt/docker/logs/syslog/` |

---

## Konzept: Zentrales Log-Verzeichnis

Alle Apps schreiben ihre Logs in `/opt/docker/logs/` auf dem Host:

```
/opt/docker/logs/
  radarr/         ← Radarr Logs
  sonarr/         ← Sonarr Logs
  jellyfin/       ← Jellyfin Logs
  ...
```

**LoVi's `docker-compose.yml`** – einmal, für alle Apps:
```yaml
volumes:
  - /opt/docker/logs:/logs
```

**Jede App bekommt nur einen zusätzlichen Volume-Eintrag**, z.B. Radarr:
```yaml
volumes:
  - /opt/docker/radarr/config:/config
  - /opt/docker/radarr/config/logs:/opt/docker/logs/radarr  # NEU
```

**LoVi muss nie angefasst werden** wenn eine neue App dazukommt. ✅

---

## Profile installieren

1. LoVi öffnen → **Settings → GitHub**
2. Gewünschtes Profil auswählen → **Install**
3. Profil steht sofort unter **Settings → Profiles** zur Verfügung

---

## Eigenes Profil beitragen

Pull Request mit einer neuen JSON-Datei im `profiles/` Ordner.
Felder: `name`, `description`, `author`, `version`, `level_error`, `level_warn`, `level_info`, `level_debug`, `log_path_hint`, `help_setup`, `help_mount`
