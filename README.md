# Twitter Unlike All

Ein JavaScript-Script, das systematisch alle Likes von einem Twitter/X-Konto entfernt. Dieses Script ist nützlich für Benutzer, die ihre Like-Historie bereinigen möchten, ohne jeden Beitrag manuell zu bearbeiten.

## Funktionsweise

- **Automatische Erkennung**: Das Script sucht nach sichtbaren "Unlike"-Buttons auf der Seite.
- **Systematisches Entfernen**: Es klickt jeden "Unlike"-Button mit einer kurzen Verzögerung, um eine Überlastung zu vermeiden.
- **Automatisches Scrollen**: Sobald alle sichtbaren Buttons verarbeitet sind, scrollt es weiter, um neue Inhalte zu laden.
- **Endlosschleife**: Das Script arbeitet, bis keine weiteren Likes mehr gefunden werden.

## Verwendung

1. Melde dich bei deinem Twitter/X-Konto an und navigiere zu deiner Like-Seite.
2. Öffne die Entwicklerkonsole (`F12` > Tab "Console").
3. Kopiere das Script und füge es in die Konsole ein.
4. Drücke "Enter", um das Script auszuführen.

## Hinweis

- Verwende dieses Script mit Vorsicht und auf eigenes Risiko.
- Beachte die Richtlinien von Twitter/X bezüglich automatisierter Interaktionen.
- Das Script wurde für persönliche Zwecke entwickelt und sollte nicht missbräuchlich eingesetzt werden.

## Beispielcode

```javascript
async function unlikeAll() {
  while (true) {
    // Finde alle sichtbaren Unlike-Buttons
    const unlikeButtons = document.querySelectorAll('button[data-testid="unlike"]');

    if (unlikeButtons.length === 0) {
      console.log('Keine weiteren Unlike-Buttons gefunden. Scrolle weiter...');
      window.scrollTo(0, document.body.scrollHeight); // Scrolle ans Ende der Seite
      await new Promise(resolve => setTimeout(resolve, 2000)); // Warte auf das Nachladen
      continue; // Wiederhole die Schleife
    }

    console.log(`Gefundene Unlike-Buttons: ${unlikeButtons.length}`);

    // Klicke jeden Button mit einer kurzen Verzögerung
    for (const button of unlikeButtons) {
      console.log('Klicke Unlike-Button:', button);

      const event = new MouseEvent('click', {
        bubbles: true,
        cancelable: true,
        view: window
      });

      button.dispatchEvent(event); // Simuliere echten Klick
      await new Promise(resolve => setTimeout(resolve, 1000)); // 1 Sekunde Pause pro Klick
    }
  }
}

unlikeAll();
