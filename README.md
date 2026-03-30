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
- Ziel: Den Namen auf der Profilkarte ändern
- Was verändern: Das Eingabefeld im Bereich "Deine Challenges"
- Ergebnis: Name wird sofort sichtbar aktualisiert

### 2. Titel ändern
- Ziel: Einen persönlichen Titel eintragen
- Was verändern: Titelfeld in der Challenge-Sektion
- Ergebnis: Titel auf der Profilkarte ändert sich live

### 3. Begrüssungstext verändern
- Ziel: Persönliche Begrüssung schreiben
- Was verändern: Textarea in der Challenge-Sektion
- Ergebnis: Begrüssung auf der Profilkarte wird aktualisiert

### 4. Hobbys ergänzen
- Ziel: Mindestens ein weiteres Hobby hinzufügen
- Was verändern: Neues Hobby eingeben und auf "Hinzufügen" klicken
- Ergebnis: Hobbyliste wächst und ist sofort sichtbar

### 5. Akzentfarbe auswählen
- Ziel: Eine andere Akzentfarbe wählen
- Was verändern: Farb-Kachel anklicken
- Ergebnis: Akzentfarbe der Website verändert sich

### 6. Button-Text ändern
- Ziel: Den Text des Profilbuttons persönlicher machen
- Was verändern: Button-Text im Challenge-Formular eingeben
- Ergebnis: Der Button-Text auf der Profilkarte aktualisiert sich

### 7. Button-Hover verbessern (Code)
- Ziel: Der Button soll interaktiver aussehen
- Was verändern: `src/App.vue` oder `src/styles.css`
- Hinweis: Ergänze einen Hover-Effekt für `.action-button`

### 8. Layout verbessern (Code)
- Ziel: Die Profilkarten sollen noch gemütlicher wirken
- Was verändern: `src/styles.css` oder `src/App.vue`
- Hinweis: Passe Abstände oder Kartendetails an

## Tipps für Betreuende

- Zeige zuerst den Bereich "Deine Challenges" und erkläre: "Du kannst hier alles direkt ändern."
- Lass die Lernenden eigene Namen, Titel und Hobbys ausprobieren.
- Für die Code-Challenges halte die Datei `src/App.vue` bereit.
- Ermutige: Kleine Änderungen führen zu sofort sichtbaren Ergebnissen.

## Ideen für Erweiterungen

- Weitere Profilfelder einbauen (Lieblingsmusik, Stadt, Lieblingsfarbe)
- Ein Foto-Upload-Platzhalter
- Mehr Challenge-Stufen mit Auszeichnungen
- Eine kleine Fortschrittsanimation
