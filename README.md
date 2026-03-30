# Schnuppern-Web

Eine kleine Vite + Vue 3 Web-App für einen Schnuppertag im Beruf Applikationsentwicklung. Die Anwendung führt Lernende durch eine Profilseite mit interaktiven UI-Challenges und endet mit zwei einfachen Code-Challenges.

## Ziel der App

- Eine moderne Profilseiten-Übung für Jugendliche
- Erste Aufgaben direkt in der Website lösen
- Sichtbare Erfolge sofort erleben
- Zum Schluss zwei kleine Code-Aufgaben direkt im Editor bearbeiten

## Zielgruppe

- Jugendliche Schnupperlernende
- wenig oder kein Vorwissen
- Einsteigerfreundlich und motivierend

## Verwendete Technologie

- Vite
- Vue 3
- HTML / CSS / JavaScript

## Voraussetzungen

- Node.js (Version 18 oder neuer empfohlen)
- npm

## Installation

1. Repository klonen oder kopieren
2. Im Projektordner installieren:

```bash
npm install
```

## Lokaler Start

```bash
npm run dev
```

Öffne dann den angegebenen lokalen Link, z. B. `http://localhost:5173`.

## Projektstruktur

- `index.html` - Einstiegsseite für Vite
- `package.json` - Projektabhängigkeiten und Skripte
- `vite.config.js` - Vite-Konfiguration
- `src/main.js` - Startpunkt der Vue-App
- `src/App.vue` - Hauptkomponente mit der gesamten Lern-App
- `src/styles.css` - globales Styling
- `solutions/challenge-solutions.md` - Lösungen für alle Challenges

## Lernkonzept und Ablauf

1. Willkommen & Erklärung
2. UI-Challenges direkt in der Oberfläche
3. Fortschrittsanzeige für den Lernenden
4. Zum Schluss zwei Code-Challenges

Die App ist so aufgebaut, dass die Lernenden zuerst Dinge direkt auf der Seite ändern. Danach können sie im Editor kleine sichtbare Verbesserungen machen.

## Übersicht der Challenges

### UI-basierte Challenges

1. Name anpassen
2. Titel ändern
3. Begrüssungstext verändern
4. Hobbys ergänzen
5. Akzentfarbe auswählen
6. Button-Text ändern

### Code-basierte Challenges

7. Button-Hover verbessern
8. Profilkarten-Abstand / Layout verbessern

## Challenges im Detail

### 1. Name anpassen
- Ziel: Einen von drei neuen Profilnamen auswählen
- Was verändern: Eine Option in der Challenge-Sektion anklicken
- Ergebnis: Der Name auf der Profilkarte verändert sich sofort

### 2. Titel ändern
- Ziel: Einen Titel aus drei Vorschlägen wählen
- Was verändern: Einen passenden Titel in der Challenge-Karte anklicken
- Ergebnis: Der Titel unter dem Namen ändert sich live

### 3. Begrüssungstext verändern
- Ziel: Einen Begrüssungsstil auswählen
- Was verändern: Eine Text-Option in der Challenge-Sektion anklicken
- Ergebnis: Der Begrüssungstext auf der Profilkarte wird angepasst

### 4. Hobbys ergänzen
- Ziel: Ein neues Hobby aus Vorschlägen wählen
- Was verändern: Ein Hobby aus der Vorschlagsliste anklicken
- Ergebnis: Die Hobbyliste erweitert sich sofort

### 5. Akzentfarbe auswählen
- Ziel: Eine andere Akzentfarbe wählen
- Was verändern: Eine Farboption in der Challenge-Karte anklicken
- Ergebnis: Die Akzentfarbe der Seite wechselt sofort

### 6. Button-Text ändern
- Ziel: Einen neuen Button-Text und Fun Fact auswählen
- Was verändern: Zwei Optionen in der Challenge-Karte anklicken
- Ergebnis: Der Profilbutton und der Fun Fact werden sichtbar aktualisiert

### 7. Button-Hover verbessern (Code)
- Ziel: Der Hauptbutton soll auf Hover lebendiger aussehen
- Was verändern: Nutze den eingebauten Editor unter "Code-Challenges"
- Hinweis: Ergänze eine Regel für `.action-button:hover`

### 8. Layout verbessern (Code)
- Ziel: Das Layout der Karten und Abstände noch gemütlicher machen
- Was verändern: Nutze den eingebauten Editor unter "Code-Challenges"
- Hinweis: Ergänze `padding`, `gap` oder `box-shadow` für `.section-card`

## Tipps für Betreuende

- Zeige zuerst den Bereich "Deine Challenges" und erkläre: "Du kannst hier alles direkt ändern."
- Lass die Lernenden eigene Namen, Titel und Hobbys ausprobieren.
- Die Code-Challenges werden direkt im virtuellen Editor der Website gelöst.
- Ermutige: Kleine Änderungen führen zu sofort sichtbaren Ergebnissen.

## Ideen für Erweiterungen

- Weitere Profilfelder einbauen (Lieblingsmusik, Stadt, Lieblingsfarbe)
- Ein Foto-Upload-Platzhalter
- Mehr Challenge-Stufen mit Auszeichnungen
- Eine kleine Fortschrittsanimation
