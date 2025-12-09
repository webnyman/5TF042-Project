# PracticeLogger IoT Extension – Projektbeskrivning

## 1. Inledning

Det här projektet syftar till att vidareutveckla *PracticeLogger Pro* genom att integrera en IoT-lösning som automatiskt kan registrera miljödata under ett övningspass. IoT-enheten mäter temperatur, luftfuktighet och ljudstyrka, och knyter dessa data till ett specifikt övningstillfälle.

Målet är att skapa ett mer heltäckande och objektivt övningssystem där användaren får återkoppling inte bara på sin egen prestation, utan också på hur omgivningsfaktorer påverkar övningskvaliteten.

---

## 2. Projektbeskrivning

### Projektidé

Systemet ska kunna:

- Starta och stoppa övningsloggning via appen eller fysisk knapp på IoT-enheten  
- Registrera temperatur, luftfuktighet, ljudnivå och tid kontinuerligt  
- Knyta alla mätvärden till ett specifikt övningspass  
- Analysera värdena efter passets slut och generera rekommendationer  
- Visualisera resultaten för användaren  

### Motivation

Projektet bygger vidare på två tidigare projekt: PracticeLogger Pro och en IoT-prototyp med Pico W. Integrationen ger ett modernt, datadrivet övningssystem.

### Målgrupp

- Musikstudenter  
- Professionella musiker  
- Musikpedagoger  
- Forskare inom övningsmetodik och ergonomi  

### Delprojekt

1. IoT-enhet  
2. Backend/API  
3. PracticeLogger GUI  
4. Analysmodul  

---

## 3. Systembeskrivning

### ER-schema (textbeskrivning)

**PracticeSession**

- SessionId (PK)  
- UserId (FK)  
- StartTime  
- EndTime  
- ManualNotes  
- Rating  
- Recommendations  

**SensorData**

- SensorDataId (PK)  
- SessionId (FK)  
- Timestamp  
- Temperature  
- Humidity  
- SoundLevel  
- IoTDeviceId (FK)

**IoTDevice**

- DeviceId (PK)  
- Name  
- OwnerUserId  
- Status  

Relationer:

- En PracticeSession har många SensorData  
- En IoTDevice kan vara kopplad till många SensorData  

### GUI-flöde

```
Start → Dashboard → Starta övning 
     → Registrering pågår
     → Stoppa övning
     → Analys
     → Historik
```

### Systemmoduler

#### IoT-modul
- Pico W  
- DHT22  
- Ljudsensor  
- Start/stopp-knapp  
- MQTT → Adafruit IO  

#### Backend/API
- /session/start  
- /session/stop  
- /sensor-data  
- Lagring + analys  

#### GUI
- Start/stopp  
- Liveindikatorer  
- Grafer  
- Rekommendationer  

---

## 4. Prioritetsordning

### Måste hinnas med
- IoT temp/fukt/ljud  
- Start/stopp  
- API + databas  
- SensorData → Session  
- Grundläggande analys  

### Bör hinnas med
- Grafer  
- Realtidsvy  

### Stretch goals
- Push-notiser  
- Flera IoT-enheter  
- PDF-export  

---

## 5. Arbetsfördelning

Projektet genomförs individuellt.

---

## 6. Tidsplan (6 veckor, slutdatum 14 jan 2026)

| Vecka | Datum | Delmoment |
|-------|--------|-----------|
| v.1 | 8–14 dec | Specifikation, diagram, GUI-skisser |
| v.2 | 15–21 dec | IoT: ljudsensor + start/stopp |
| v.3 | 22–28 dec | Backend/API + databas |
| v.4 | 29 dec–4 jan | GUI utveckling |
| v.5 | 5–11 jan | Analys + grafer |
| v.6 | 12–14 jan | Test, dokumentation, demo |

---

## 7. Systemarkitektur

Översiktligt flöde:

```
Pico W → MQTT Publish → Adafruit IO Feeds → REST GET → .NET / PracticeLogger → DB/CSV
```

Diagram finns i filen `iot-architecture-labeled-arrows.svg`.

---

## 8. ER-diagram

Se `er-diagram.svg`.

---

## 9. GitHub Issues

### Vecka 1
- [ ] Kravspec  
- [ ] Arkitekturdiagram  
- [ ] ER-diagram  
- [ ] GUI-flöden  

### Vecka 2
- [ ] Ljudsensor  
- [ ] Start/stopp  
- [ ] MQTT stabilisering  
- [ ] Dokumentation  

### Vecka 3
- [ ] Databasmodell  
- [ ] API: start session  
- [ ] API: stop session  
- [ ] API: sensor-data  
- [ ] Integrationstest  

### Vecka 4
- [ ] GUI start/stopp  
- [ ] Visa status  
- [ ] Koppla GUI till API  
- [ ] Sessionshistorik  

### Vecka 5
- [ ] Analys (temp/fukt/ljud)  
- [ ] Grafer  
- [ ] Rekommendationer  

### Vecka 6
- [ ] End-to-end-test  
- [ ] Kodstädning  
- [ ] Uppdaterad README  
- [ ] Videodemonstration  
- [ ] Slutlig leverans  

