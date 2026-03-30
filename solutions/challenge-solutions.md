# Challenge-Lösungen

Dieses Dokument zeigt zu jeder Challenge eine einfache Lösung. Die Aufgaben sind bewusst klein und gut verständlich.

## UI-Challenges

### 1. Name im Code setzen
- Öffne die Seite im Browser.
- Wähle in der Code-Challenge den korrekten Code-Snippet aus, der `profile.name` setzt.
- Ergebnis: Der Profilname oben links ändert sich sofort.

### 2. Titel im Code setzen
- Wähle in der Code-Challenge die richtige Code-Zeile, die `profile.title` setzt.
- Ergebnis: Der Titel unter dem Namen aktualisiert sich live.

### 3. Begrüssungstext im Code setzen
- Wähle in der Code-Challenge die richtige Zeile, die `profile.greeting` setzt.
- Ergebnis: Der Begrüssungstext erscheint sofort angepasst.

### 4. Hobby per Code hinzufügen
- Wähle in der Code-Challenge die richtige Code-Zeile, die ein Hobby zur Liste hinzufügt.
- Ergebnis: Das Hobby erscheint in der Liste und erweitert das Profil.

### 5. Accent-Farbe per Code ändern
- Wähle in der Code-Challenge die richtige Zeile, die `profile.accent` ändert.
- Ergebnis: Die Akzentfarbe der Seite wechselt sofort.

### 6. Profiltext per Code ändern
- Wähle in der Code-Challenge die richtige Zeile, die `profile.buttonText` und `profile.funFact` setzt.
- Ergebnis: Der Profilbutton und der Fun Fact werden direkt aktualisiert.

## Code-Challenges

### 7. Button-Hover verbessern
- Aufgabe: Nutze den eingebauten Code-Editor auf der Website.
- Suche im Editor die Stelle mit `/* TODO: Ergänze hier den Hover-Effekt für den Button */`.
- Ergänze eine Hover-Regel für `.action-button:hover`.

Beispiel:

```css
.action-button:hover {
  transform: translateY(-1px);
  box-shadow: 0 18px 36px rgba(92, 124, 250, 0.18);
}
```

Das macht den Button spürbar interaktiver.

### 8. Layout / Abstände verbessern
- Aufgabe: Nutze den eingebauten Code-Editor auf der Website.
- Suche im Editor die Stelle mit `/* TODO: Mache die Karten noch gemütlicher mit mehr Abstand oder Schatten */`.
- Ergänze `padding`, `gap` oder `box-shadow` für `.section-card`, damit das Layout gemütlicher wirkt.

Beispiel:

```css
.section-card {
  padding: 28px;
  gap: 24px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.12);
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
