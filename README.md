⚡ Solakon Master–Follower Blueprint
1–3 Solakon One Inverter · NT/HT Tariflogik · Phasenbasiert · SAFE MODE
https://img.shields.io/badge/Home%20Assistant-Blueprint-41BDF5?style=for-the-badge
https://img.shields.io/badge/Solakon-One-orange?style=for-the-badge
https://img.shields.io/badge/Safety-First-green?style=for-the-badge
https://img.shields.io/badge/Version-1.0.0-blue?style=for-the-badge
https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge
https://img.shields.io/badge/Status-Stable-brightgreen?style=for-the-badge

📥 Blueprint direkt importieren
Import Blueprint (my.home-assistant.io in Bing)

🔍 Überblick
Dieser Blueprint steuert 1–3 Solakon One Wechselrichter in einem intelligenten Master–Follower‑System:

Master führt, Follower unterstützen dynamisch

NT/HT‑Tariflogik

Phasenbasierte Leistungssteuerung

Gemeinsames SoC‑Management (20–90 %)

SAFE MODE bei Sensorfehlern

Keine Einspeisung, keine Überlastung, keine Oszillation

Der Blueprint nutzt die offiziellen Solakon Remote‑Control‑Entities und ist vollständig kompatibel mit der Solakon One Integration.

🖼 Screenshots (Platzhalter)
Du kannst später echte Screenshots einfügen.
Diese Platzhalter bleiben, bis du sie ersetzt.

Blueprint‑Import
[Anscheinend war das Ergebnis nicht sicher anzuzeigen. Lassen Sie uns die Dinge ändern und etwas anderes ausprobieren!]

Blueprint‑Konfiguration
[Anscheinend war das Ergebnis nicht sicher anzuzeigen. Lassen Sie uns die Dinge ändern und etwas anderes ausprobieren!]

Automations‑Übersicht
[Anscheinend war das Ergebnis nicht sicher anzuzeigen. Lassen Sie uns die Dinge ändern und etwas anderes ausprobieren!]

🧠 Funktionsweise
🔋 SoC‑Fenster
20–90 %

NT‑Ziel: 80 %

🕒 NT/HT‑Logik
NT → Laden erlaubt

HT → Entladen nur bei Netzbezug

HT → Laden nur bei PV‑Überschuss

⚡ Phasenbasierte Leistung
0–1200 W pro Inverter

Optimalbereich: 600–800 W

Jede Phase wird separat betrachtet

👑 Master–Follower
Follower laden nur, wenn Master‑SoC > 70 %

Follower entladen nur, wenn Master‑SoC > 50 %

Master hat immer Priorität

🛡 SAFE MODE
SAFE MODE wird aktiviert, wenn:

Sensorwerte unknown / unavailable

SoC‑Werte fehlen

Phasenleistung fehlt

Total Power fehlt

SAFE MODE Verhalten:

Alle Inverter → Battery Charge

Leistung = 0

Timeout = 60 s

Notification in Home Assistant

🏗 Architektur
Code
                   ┌──────────────────────────────┐
                   │        Shelly 3EM             │
                   │  (Total + Phase Power)        │
                   └──────────────┬───────────────┘
                                  │
                                  ▼
                     ┌────────────────────────┐
                     │   Blueprint Logic       │
                     │  - NT/HT               │
                     │  - SoC Window          │
                     │  - Phase Power         │
                     │  - Master–Follower     │
                     │  - SAFE MODE           │
                     └────────────┬──────────┘
                                  │
         ┌────────────────────────┼────────────────────────┐
         ▼                        ▼                        ▼
┌────────────────┐     ┌────────────────┐     ┌────────────────┐
│ Solakon Master │     │ Solakon F1     │     │ Solakon F2     │
│ Mode + Power   │     │ Mode + Power   │     │ Mode + Power   │
└────────────────┘     └────────────────┘     └────────────────┘
