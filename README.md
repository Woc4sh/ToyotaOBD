# Toyota Hybrid Energy Monitor - Android App

## Struktura projektu

```
HybridMonitor/
├── app/
│   ├── build.gradle
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/hybridmonitor/
│       │   ├── MainActivity.kt         ← Połączenie BT + OBD2
│       │   └── EnergyFlowView.kt       ← Animowany monitor energii
│       └── res/
│           ├── layout/
│           │   ├── activity_main.xml
│           │   └── card_stat.xml
│           ├── drawable/
│           │   ├── card_bg.xml
│           │   └── spinner_bg.xml
│           └── values/
│               ├── strings.xml
│               └── themes.xml
├── build.gradle
└── settings.gradle
```

## Wymagania

- **Adapter OBD2 Bluetooth** (ELM327 v1.5 lub nowszy)
  - Zalecany: Veepeak OBDCheck BLE+ lub Vgate iCar Pro BT4.0
  - Upewnij się, że adapter jest sparowany z telefonem przed uruchomieniem aplikacji
- Android 6.0+ (API 23)
- Toyota Hybrid (Prius, Yaris Cross, Corolla Hybrid, C-HR, RAV4 Hybrid itp.)

## Jak uruchomić

1. Otwórz projekt w **Android Studio (Hedgehog lub nowsze)**
2. `File → Open` → wybierz folder `HybridMonitor`
3. Poczekaj na sync Gradle
4. Połącz telefon przez USB lub uruchom emulator
5. Kliknij **Run ▶**

## Dostępne dane

| Parametr | PID OBD | Opis |
|---|---|---|
| Prędkość | `010D` | km/h |
| Obroty silnika | `010C` | RPM |
| Temperatura płynu | `0105` | °C |
| Obciążenie silnika | `0104` | % |
| Gaz | `0111` | % |
| Napięcie 12V | `ATRV` | V |
| Bateria HV SOC | `2161` | % (Toyota custom PID) |
| Moc motoru MG2 | `2162` | kW (Toyota custom PID) |

## Tryby monitora energii

| Tryb | Opis |
|---|---|
| ⚡ TRYB EV | Jazda tylko na silniku elektrycznym |
| 🔥 SILNIK + MOTOR | Silnik spalinowy + wspomaganie elektryczne |
| 🔥 SILNIK (ŁADOWANIE) | Silnik ładuje baterię HV |
| ⟳ REKUPERACJA | Odzysk energii podczas hamowania |
| ○ POSTÓJ | Pojazd stoi |

## Uwagi

- **Toyota custom PIDs** (`21xx`) mogą nie działać na wszystkich adapterach - 
  wymagany protokół CAN z obsługą trybu 21.
- Jeśli SOC baterii pokazuje stałą wartość, adapter nie obsługuje tych PIDów.
- Aplikacja nie wymaga roota ani dodatkowego oprogramowania.
