# solakon-master-follower-blueprint
solakon-master-follower-blueprint
⚡ Solakon Master–Follower Blueprint
1–3 Solakon One Inverter · NT/HT Tariflogik · Phasenbasiert · SAFE MODE
https://img.shields.io/badge/Home%20Assistant-Blueprint-41BDF5?style=for-the-badge
https://img.shields.io/badge/Solakon-One-orange?style=for-the-badge
https://img.shields.io/badge/Safety-First-green?style=for-the-badge

🔍 Überblick
Dieser Blueprint steuert 1–3 Solakon One Wechselrichter in einem intelligenten Master–Follower‑System:

Master führt, Follower unterstützen dynamisch

NT/HT‑Tariflogik (Niedertarif / Hochtarif)

Phasenbasierte Leistungssteuerung (Shelly 3EM oder vergleichbar)

Gemeinsames SoC‑Management (20–90 %)

SAFE MODE bei Sensorfehlern

Keine Einspeisung, keine Überlastung, keine Oszillation

Der Blueprint nutzt die offiziellen Solakon Remote‑Control‑Entities und ist vollständig kompatibel mit der Solakon One Integration.

🎯 Ziele
Maximale Eigenverbrauchsquote

Batterieschutz (kein Tiefentladen, kein Überladen)

Stabile, vorhersagbare Logik

Automatische Fehlererkennung

Perfekte Balance zwischen mehreren Inverter‑Batterien

🧠 Funktionsweise
1. Messung & Eingänge
Der Blueprint nutzt:

🔌 Shelly‑Sensoren
Total Power → Netzbezug / Einspeisung

Phasenleistung → pro Phase (L1/L2/L3)

🔋 SoC‑Sensoren
Master SoC

Follower 1 SoC (optional)

Follower 2 SoC (optional)

⚙️ Solakon‑Remote‑Control‑Entities
select.solakon_one_remote_control_mode

number.solakon_one_remote_active_power_control

number.solakon_one_minimum_soc_control

number.solakon_one_maximum_soc_control

number.solakon_one_minimum_soc_ongrid_control

number.solakon_one_remote_timeout_control

2. Kernlogik
🔋 SoC‑Fenster
20 % – 90 % für alle Inverter

NT‑Ziel: 80 %

🕒 NT/HT‑Tariflogik
NT:

Laden aus Netz erlaubt

Keine Entladung

HT:

Entladen nur bei Netzbezug

Laden nur aus PV‑Überschuss

⚡ Phasenbasierte Leistung
Jede Phase wird separat betrachtet

Leistung pro Inverter: 0–1200 W

Optimalbereich: 600–800 W

👑 Master–Follower‑Regeln
Follower laden nur, wenn Master‑SoC > 70 %

Follower entladen nur, wenn Master‑SoC > 50 %

Master hat immer Priorität

3. SAFE MODE
SAFE MODE wird aktiviert, wenn:

Sensorwerte unknown / unavailable sind

SoC‑Werte fehlen

Phasenleistung fehlt

Total Power fehlt

SAFE MODE Verhalten:

Alle Inverter → Battery Charge

Leistung → 0 W

Timeout → 60 s

Notification in Home Assistant
