# Weihnachtsboard einrichten

Das Board ist eine Webseite, die jeder ohne Anmeldung öffnen und ausfüllen kann.
Die Seite liegt bei GitHub Pages, die Einträge in einer Firebase-Datenbank von Google.
Beides ist kostenlos. Einmal einrichten dauert etwa 15 Minuten.

## 1. Firebase-Datenbank anlegen (Google-Konto nötig)

1. Öffne <https://console.firebase.google.com> und melde dich mit deinem Google-Konto an.
2. **Projekt erstellen** (oder „Firebase-Projekt erstellen“). Als Name zum Beispiel `weihnachtsboard`.
   Google Analytics brauchst du nicht: ausschalten und **Projekt erstellen**.
3. Im linken Menü **Build > Firestore Database** (manchmal unter „Datenbanken und Speicher“) öffnen, dann **Datenbank erstellen**.
   - Edition, falls gefragt: **Standard**.
   - Standort: `eur3 (europe-west)` oder `europe-west3 (Frankfurt)`.
   - Modus: **Im Produktionsmodus starten**. Dann **Erstellen**.
4. In der Firestore-Datenbank den Tab **Regeln** öffnen. Alles dort löschen, den Inhalt der Datei
   [`firestore.rules`](firestore.rules) aus diesem Repo einfügen und auf **Veröffentlichen** klicken.
5. Oben links auf das Zahnrad > **Projekteinstellungen**. Unten bei „Meine Apps“ auf das Symbol **`</>`** (Web) klicken.
   - App-Name: `Weihnachtsboard`. „Firebase Hosting“ **nicht** anhaken. **App registrieren**.
   - Es erscheint ein Code-Block mit `const firebaseConfig = { apiKey: ..., projectId: ..., ... };`.
     Kopiere nur den Teil von `{` bis `}`.

## 2. Zugangsdaten eintragen

Trage den kopierten Block in [`firebase-config.js`](firebase-config.js) ein, sodass die Zeile so aussieht:

```js
export const firebaseConfig = {
  apiKey: "…",
  authDomain: "….firebaseapp.com",
  projectId: "…",
  storageBucket: "…",
  messagingSenderId: "…",
  appId: "…"
};
```

Oder schick den Block an Claude, dann wird er eingetragen. Die Werte sind nicht geheim: Sie sagen der
Seite nur, welche Datenbank sie benutzen soll.

## 3. Webseite bei GitHub Pages veröffentlichen

GitHub Pages ist bei einem kostenlosen GitHub-Konto nur für öffentliche Repos verfügbar.

1. Repo auf GitHub öffnen > **Settings** > ganz unten **Danger Zone** > **Change visibility** > **Public**.
2. **Settings** > **Pages**: Bei „Source“ **Deploy from a branch** wählen, Branch **`claude/weihnachtsboard`**, Ordner **`/ (root)`**, **Save**.
3. Nach ein bis zwei Minuten ist das Board erreichbar unter
   **<https://rvk5529nw4-ui.github.io/Weihnachtsboard/>**.
   Diesen Link an die Familie schicken.

## Gut zu wissen

- **Jeder mit dem Link** kann lesen und ändern, ohne Anmeldung. Den Link also nur in der Familie teilen.
- Ändern ist bis **31. Januar 2027** möglich, danach kann man nur noch lesen. Zum Verlängern das Datum in den Regeln anpassen und neu veröffentlichen.
- Das Repo ist öffentlich. Wer es findet, sieht den Code und die Vornamen, aber nicht die Einträge im Board.
  Die Seite ist für Suchmaschinen gesperrt (`noindex`).
- Der kostenlose Firebase-Tarif reicht für eine Familie bei weitem aus.
- `claude-board.html` ist die alte Version für Claude und wird für die Webseite nicht gebraucht.
