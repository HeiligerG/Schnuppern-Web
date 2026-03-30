# Challenge-Lösungen

Dieses Dokument zeigt zu jeder Challenge eine einfache Lösung. Die Aufgaben sind bewusst klein und gut verständlich.

## UI-Challenges

### 1. Name anpassen
- Öffne die Seite im Browser.
- In der Challenge-Sektion unter "Name anpassen" einen neuen Namen anklicken.
- Ergebnis: Der Profilname oben links ändert sich sofort.

### 2. Titel ändern
- Wähle einen neuen Titel aus der Liste in der Challenge-Karte.
- Ergebnis: Der Titel unter dem Namen aktualisiert sich live.

### 3. Begrüssungstext verändern
- Wähle einen Begrüssungstext aus den vorgeschlagenen Optionen.
- Ergebnis: Der Text im Profil erscheint sofort angepasst.

### 4. Hobbys ergänzen
- Wähle eines der vorgeschlagenen Hobbys aus.
- Ergebnis: Das Hobby erscheint in der Liste und erweitert das Profil.

### 5. Akzentfarbe wählen
- Klicke auf eine der Farboptionen: Blau, Grün oder Lila.
- Ergebnis: Das Farbschema der Buttons und des Designs wechselt.

### 6. Button-Text ändern
- Wähle einen neuen Button-Text und einen Fun Fact aus den Vorschlägen aus.
- Ergebnis: Der Profilbutton und der Fun Fact werden direkt aktualisiert.

## Code-Challenges

### 7. Button-Hover verbessern
- Datei: `src/styles.css`
- Suche die Regel für `.action-button`.
- Ergänze einen Hover-Zustand mit einem sanften Schatten oder Farbwechsel.

Beispiel:

```css
.action-button:hover {
  transform: translateY(-1px);
  box-shadow: 0 18px 36px rgba(92, 124, 250, 0.18);
}
```

Das macht den Button fühlbar interaktiver.

### 8. Layout / Abstände verbessern
- Datei: `src/styles.css`
- Suche die allgemeine Kartengestaltung oder die `.section-card`-Regel.
- Erhöhe den `padding`-Wert oder passe `gap` an, damit die Karte gemütlicher wirkt.

Beispiel:

```css
.section-card {
  padding: 28px;
  gap: 24px;
}
```

Oder ergänze:

```css
.profile-top {
  gap: 20px;
}
```

Damit wirkt die Profilkarte räumlicher und angenehmer.

## Hinweise für saubere Lösungen

- Die ersten sechs Challenges sind direkt in der Website sicht- und erfüllbar.
- Bei Code-Challenges wird nicht das Verhalten geändert, sondern das Aussehen der App verbessert.
- Kleine Style-Änderungen sind perfekt für Schnupperlernende: sie sehen sofort das Ergebnis.

## Schöne Variante für Challenge 8

Zusätzlich zur einfachen Abstandsverbesserung kannst du auch eine weichere Box-Shadow hinzufügen:

```css
.section-card {
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.12);
}
```

So wirkt die Oberfläche moderner und leichter.
