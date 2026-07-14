# 🅿️ Smart Parking System
 

Lucrarea de față prezintă proiectarea și implementarea unui sistem inteligent de gestionare a parcărilor (*Smart Parking System*), destinat ușurării procesului de monitorizare, control al accesului și tarifare a unui spațiu de parcare. Soluția propusă integrează componente hardware și software într-un sistem coerent și funcțional, capabil să detecteze în timp real starea locurilor de parcare, să controleze accesul vehiculelor prin intermediul unei bariere automatizate și să calculeze automat tarifele de staționare.
 
## Cuprins
 
- [Descriere generală](#-descriere-generală)
- [Componente hardware](#-componente-hardware)
- [Macheta](#-macheta)
- [Firmware Arduino](#-firmware-arduino)
- [Aplicația Android](#-aplicația-android)
- [Interfața grafică](#-interfața-grafică)

 
## Descriere generală
 
Senzorii colectează datele de pe machetă și le trimit la Arduino, Arduino trimite datele mai departe către Bluetooth, iar Bluetooth le trimite către aplicația mobilă.
 
<p align="center">
  <img width="500" alt="Diagrama de flux a sistemului" src="https://github.com/user-attachments/assets/def32f21-fcf1-4b66-bc73-29020c9bb069" />
</p>

 
## Componente hardware
 
| Componentă | Rol |
|---|---|
| Arduino Mega 2560 | Unitatea centrală de procesare |
| Modul Bluetooth HC-05 | Comunicare Arduino ↔ Android |
| 6 x senzori obstacol IR | Detectare ocupare loc de parcare |
| Servo SG90 | Acționare barieră |
| LCD I2C | Afișaj local |
| Senzor gaz MQ-5 | Detectare scurgeri de gaz |
| Senzor de nivel | Monitorizare suplimentară |
| Buzzer pasiv | Alarmă sonoră |
 

 
## Macheta
 
Macheta a fost construită pe o suprafață plană, elevată, pentru a permite un acces mai ușor la componentele hardware, reprezentând schematic un spațiu de parcare cu 6 locuri individuale, aranjate în două rânduri de câte 3.
 
<p align="center">
  <img width="500" alt="Macheta fizică a sistemului" src="https://github.com/user-attachments/assets/e8761dfa-8c70-4b39-811f-fa70ce7421cb" />
</p>

 
## Firmware Arduino
 
Firmware-ul Arduino (prezentat integral în [Anexa A](./Anexa%20A.txt))  este organizat conform paradigmei standard Arduino: funcția `setup()`, executată o singură dată la pornire, și funcția `loop()`, care rulează continuu.
 
Diagrama de flux a funcționării firmware-ului Arduino este următoarea:
 
<p align="center">
  <img width="380" alt="Diagrama de flux a firmware-ului" src="https://github.com/user-attachments/assets/a7b64bd6-1acb-4c3b-bb20-b45f33834fc0" />
</p>

 
## Aplicația Android
 
**IDE și mediu de dezvoltare:** Android Studio
 
Aplicația mobilă a fost dezvoltată de la zero în Android Studio, folosind **Java** ca limbaj principal pentru logica aplicației. Am ales acest stack pentru că oferă control direct asupra componentelor native Android (Bluetooth, UI, threading), esențial pentru comunicarea în timp real cu microcontrolerul.
 
**Structura aplicației:**
 
- **Activities & UI** — interfața principală afișează disponibilitatea locurilor de parcare în timp real, actualizată dinamic pe măsură ce datele sosesc de la Arduino
- **Bluetooth Communication Layer** — comunicare cu modulul HC-05 folosind `BluetoothSocket` și `BluetoothAdapter` din Android SDK, pentru a trimite/primi date către/de la microcontroler
- **Data parsing** — logica de interpretare a datelor primite (starea celor 6 senzori IR, alertele de gaz) și actualizarea interfeței corespunzător
- **Control de la distanță** — comenzi trimise către servomotor pentru deschiderea/închiderea barierei, direct din aplicație

 
##  Interfața grafică
 
Interfața grafică a aplicației cuprinde o bară de navigație inferioară cu trei tab-uri (**PARCARE**, **ISTORIC** și **SETĂRI**), o grilă de 6 locuri de parcare codificate cromatic, un panou de informații cu numărul de locuri libere și butoanele **INTRARE / IEȘIRE / PLATĂ**, și un panou de status care afișează ultimul eveniment produs. Codificarea cromatică (verde = liber, roșu = ocupat) este intuitivă și conformă cu convenția internațională din parcările convenționale. Codul este disponibil in [Anexa B](./Anexa%20B.txt).
 
<p align="center">
  <img width="220" alt="Ecran principal - locuri de parcare" src="https://github.com/user-attachments/assets/b14becf3-0f84-4dfe-8f71-a154af41d6ff" />
  &nbsp;&nbsp;
  <img width="220" alt="Actualizare stare locuri în timp real" src="https://github.com/user-attachments/assets/2a44fcb5-fdf8-4229-ae78-15a1d683ef16" />
  &nbsp;&nbsp;
  <img width="220" alt="Dialog intrare parcare - numar de inmatriculare" src="https://github.com/user-attachments/assets/7d850e4a-4f67-4b16-b92d-2bdac617d4d6" />
</p>
<p align="center">
  <em>Stânga → dreapta: grilă locuri de parcare · actualizare în timp real a stării locurilor · dialog de introducere a numărului de înmatriculare (ex. BZ 01 GDI)</em>
</p>

