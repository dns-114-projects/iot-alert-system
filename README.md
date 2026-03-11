# IoT Embedded Alert System — Détecteur Sismique

**Projet IoT** | école d'ingénieurs — Nov. 2025–Jan. 2026 | Lua 5.3, ESP32, LuaRTOS

## Contexte

Conception d'un sismòmetre bas coût autonome basé sur ESP32, capable de détecter des ondes sismiques de type P et d'envoyer des alertes en temps réel via Telegram. Application cible : infrastructures critiques (datacenters, hôpitaux, sous-stations).

## Matériel

| Composant | Rôle |
|:---|:---|
| ESP32 (MCU) | Traitement central, WiFi, gestion des interruptions |
| Capteur Hall magnétique | Détection des vibrations mécaniques |
| Aimant + ressort | Masse oscillante simulant un pendule sismique |
| Écran OLED 128×64 | Affichage local du statut et du dernier événement |

## Architecture logicielle

Langage : **Lua 5.3.4 + LuaRTOS**. Modules utilisés : `pio` (GPIO/interruptions), `i2c` (OLED), `net.wf` (WiFi), `net.curl` (HTTP/HTTPS), `tmr`, `thread`, `os`.

### Détection
- **Interrupt-driven** — réponse temps-réel sans polling
- **Classification multi-niveaux** — seuils bas/moyen/haut selon intensité
- **Analyse de durée** — distinction séisme vs choc accidentel
- **Logging JSON horodaté** de chaque événement

### Alertes (Telegram Bot API)
- Alerte sismique majeure (critique)
- Pré-alerte modérée (info)
- Détection anomalie (distinction choc/séisme)
- **Résilience** : buzzer local fonctionnel si WiFi indisponible

## Queue d'événements

```
Capteur Hall
    → Interruption GPIO
    → Thread de traitement (analyse durée + classification)
    → [OLED + Buzzer] + [Telegram HTTP/HTTPS]
    → Logging JSON
```

## Stack

`Lua 5.3` · `LuaRTOS` · `ESP32` · `Telegram Bot API` · `I2C/OLED`

---

*Projet académique — école d'ingénieurs*
