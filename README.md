# Testaufgabe: SIP-Client in Docker mit Audio-Stream-Verarbeitung

## Ziel
Entwickle einen Docker-Container, der sich bei einem SIP-Server anmeldet, ausgehende Anrufe über eine REST-API triggert und Audio-Daten über WebSockets bereitstellt. 
Es reicht die Machbarkeit nachzuweisen. Die Lösung soll ohne spezielle Hardware-Anforderungen laufen.  
  
Wichtig! Nur die PORTS und die Funktionen sollen passen.  
Innerhalb des Containers kannst du jedes Tool, jede Lib nutzen oder selber Software entwickeln. 

## Anforderungen

1. **Docker-Setup**
   - Erstelle einen Docker-Container und eine `docker-compose.yml`.
   - Basis-Image: Bevorzugt Alpine (falls möglich), sonst Ubuntu.
   - Bitte keine speziellen Hardware-Argumente (kein Zugriff auf Host-Hardware, modprobe etc.).

2. **SIP-Anmeldung**
   - Die Software im Container meldet sich bei einem SIP-Server (z. B. Fonial) an.
   - Konfiguration über Umgebungsvariablen (z. B. in `.env`).
   - Nutze Bibliotheken! Wir haben uns per `pjsua2` oder `baresip` auf unseren Telefon-Provider verbinden können (Achtung: kein WebRTC/SIP.js verwenden! WebRTC wird oft nichts unterstützt).

3. **REST-API**
   - API-Route auf Port `8085`.
   - Endpunkt zum Triggern eines ausgehenden Anrufs (z. B. `POST /call` mit Zielnummer im Body).
   - Hierzu muss evtl. ein mini Webserver gebaut werden, der dann den SIP Client ansteuert.

4. **WebSocket-Verbindungen**
   - Port `8086`: WebSocket zum Senden von Audio-Daten, die über SIP an den Angerufenen übertragen werden.
   - Port `8087`: WebSocket zum Empfangen des Audio-Datenstreams vom Angerufenen.
   - Audio-Format: Beliebig (z. B. WAV/Opus), aber konsistent.

5. **Dokumentation & Tests**
   - `README.md`: Anleitung zum Build, Start und Test des Containers.
   - Testskript: Skript (z. B. Python/Bash) zum Testen der API und WebSocket-Verbindungen.

## Hinweise
- Die Wahl der Software und des Betriebssystems innerhalb des Containers ist absolut und vollkommen frei. Du kannst beliebige Bibliotheken verwenden, solange die äußeren Bedingungen außerhalb des Containers (Ports, API, WebSockets) erfüllt sind.
- `pjsua2` und `baresip` können SIP-Anmeldung und Anrufe handhaben, bieten aber keinen einfachen Zugriff auf Audio-Datenstreams. Finde eine Lösung, um Audio-Daten zu extrahieren und über WebSockets bereitzustellen.
- Der Container muss eigenständig laufen und Audio über virtuelle Devices (keine Hardware) verarbeiten.

## Abgabe
- Code und Konfiguration in einem Git-Repository.
- Bitte stelle einen Link zu einem öffentlichen oder privaten GitHub-Repository bereit.
- `README.md` mit klaren Anweisungen.
- Testskript zum Nachweis der Funktionalität.

## Bewertungskriterien
- Funktionalität (SIP-Anmeldung, Anruf, Audio-Streams).
- Effizienz (Image-Größe, Ressourcennutzung).
- Code-Qualität und Dokumentation.
- Einhaltung der Vorgaben (keine Hardware-Abhängigkeiten).

Viel Erfolg!
