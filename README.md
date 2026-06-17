<div align="center">

# ESP32-CaptivePortal

**Catch-all Captive Portal für ESP32** — DNS-Wildcard + WebServer, sodass Geräte/OSe das WLAN als „captive" erkennen und automatisch die Portalseite öffnen.

[![Plattform](https://img.shields.io/badge/Plattform-ESP32-blue?style=flat-square)](.)
[![Build](https://img.shields.io/badge/Build-PlatformIO%20(pioarduino)-orange?style=flat-square&logo=platformio)](https://platformio.org)
[![Core](https://img.shields.io/badge/Arduino--ESP32-3.1.x-green?style=flat-square)](.)
[![Lizenz](https://img.shields.io/badge/Lizenz-MIT-green?style=flat-square)](LICENSE)

</div>

---

Der ESP32 spannt einen Access-Point (`ESP32-DNSServer`) auf und beantwortet **jede** DNS-Anfrage mit seiner eigenen IP. Dadurch erkennen Android, Windows, Ubuntu, Firefox u.a. das Netz als Captive Portal und öffnen die Banner-Seite automatisch — ohne dass man `http://192.168.4.1` manuell aufrufen muss. Lab-Demo und Basis für Awareness-Portale.

## Funktion

| Komponente | Aufgabe |
|------------|---------|
| **DNSServer** | Catch-all (`*`) → liefert AP-IP für jede Domain |
| **WebServer** | `/` Begrüßung, `/portal` Banner-Seite, alle unbekannten Pfade → Redirect aufs Portal |
| **WiFi.AP** | Access-Point + (ab Core 3.2) DHCP-Captive-Portal-Signalisierung (RFC 8910) |

## Fertige Firmware

Vorkompiliertes Image unter [**Releases**](https://github.com/G4MEOVER18/ESP32-CaptivePortal/releases/latest):

```bash
esptool.py --chip esp32 write_flash 0x0 ESP32-CaptivePortal_esp32_v1.0.0_merged.bin
```

Danach mit dem WLAN **`ESP32-DNSServer`** verbinden — die Portalseite öffnet sich automatisch.

## Selbst bauen (PlatformIO)

```bash
pio run                       # bauen
pio run -t upload             # flashen
pio device monitor -b 115200  # serielle Ausgabe
```

Der Sketch nutzt die **Core-3.x `WiFi.AP`-API** (`WiFi.AP.create`), die das offizielle PlatformIO (Core 2.x) nicht bietet — daher die **pioarduino**-Plattform (gepinnt). `enableDhcpCaptivePortal()` (ab Core 3.2) ist per Versions-Guard optional; der DNS-Catch-All genügt zur Erkennung. Keine externen Libraries. Details: [`docs/DEPENDENCIES.md`](docs/DEPENDENCIES.md).

## Hinweis

Nur in eigenen Netzen / Laboren einsetzen. Ein Captive Portal fängt fremden Traffic ab — Nutzung gegen Dritte ohne Einwilligung ist unzulässig.

## Lizenz

MIT – siehe [LICENSE](LICENSE). © 2026 Yanis Ameseder

---

## Kontakt

**Entwickler:** Yanis Ameseder · **E-Mail:** [g4me.over.18@gmail.com](mailto:g4me.over.18@gmail.com)
