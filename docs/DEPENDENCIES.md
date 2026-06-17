# Abhängigkeiten

Reproduzierbarer Build über **PlatformIO** mit der **pioarduino**-Plattform
(Arduino-ESP32 Core 3.1.x). Version in `platformio.ini` gepinnt.

| Abhängigkeit | Version | Zweck |
|--------------|---------|-------|
| Plattform `pioarduino` | `53.03.13` | Arduino-ESP32 Core 3.1.x (für `WiFi.AP`-API) |

**Keine externen Libraries** — der Sketch nutzt ausschließlich den ESP32-Arduino-Core:
`WiFi`, `DNSServer`, `WebServer`.

## Warum pioarduino?

Der Sketch verwendet die in **Core 3.x** eingeführte `WiFi.AP`-API
(`WiFi.AP.begin()` / `WiFi.AP.create()`). Das offizielle PlatformIO
(`espressif32`) liefert nur Core 2.x mit der alten `WiFi.softAP()`-API.

`WiFi.AP.enableDhcpCaptivePortal()` (DHCP-/RFC-8910-Signalisierung) gibt es erst
ab Core 3.2.0 und ist daher per `ESP_ARDUINO_VERSION`-Guard optional gekapselt —
der DNS-Catch-All genügt zur Captive-Portal-Erkennung.
