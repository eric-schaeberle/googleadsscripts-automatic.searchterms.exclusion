Dieses Skript für Google Ads ermöglicht die automatische Identifikation und den Ausschluss von Suchbegriffen, die mehr als 100 Impressionen aber keine Klicks generiert haben. Durch das Hinzufügen dieser Begriffe als exakte negative Keywords zu einer spezifischen Liste werden Ihrer Zielgruppe genauer getroffen, wodurch Ihre Anzeigenrelevanz kontinuierlich verbessert wird.

## Hauptfunktionen
Analyse von Suchbegriffen: Ermittelt Suchbegriffe mit über 100 Impressionen und 0 Klicks.
Verwaltung negativer Keyword-Listen: Überprüft, ob eine bestimmte negative Keyword-Liste existiert, und erstellt diese bei Bedarf.
Exakte Übereinstimmung: Fügt die identifizierten Suchbegriffe als exakte negative Keywords zur Liste hinzu.

## Funktionsweise
Das Skript führt eine Abfrage in der search_term_view durch, um Suchbegriffe mit mehr als 100 Impressionen und keinen Klicks zu finden. Es überprüft, ob eine negative Keyword-Liste mit dem Namen "Keywords über 100 Impressionen ohne Klicks" existiert. Falls nicht, wird eine solche Liste erstellt. Anschließend werden die identifizierten Keywords als exakte Übereinstimmungen in die Liste eingefügt.

### Einleitung und Abfrage
```javascript
// Abfrage, um Suchbegriffe mit mindestens 100 Impressionen und keinen Klicks zu finden
const report = AdsApp.report(
    `SELECT search_term_view.search_term, ` +
    `metrics.impressions, metrics.clicks ` +
    `FROM search_term_view ` +
    `WHERE metrics.impressions >= 100 ` +
    `AND metrics.clicks = 0`);
```
Dieser Abschnitt führt eine Abfrage in der search_term_view von Google Ads durch. Es werden Suchbegriffe ausgewählt, die mindestens 100 Impressionen aber keine Klicks erhalten haben. Diese Suchbegriffe sind potenzielle Kandidaten für den Ausschluss.

### Sammeln der Suchbegriffe
```javascript
const rows = report.rows();
const keywordsToExclude = [];

while (rows.hasNext()) {
  var row = rows.next();
  var keywordQuery = row['search_term_view.search_term'];
  keywordsToExclude.push(keywordQuery);
}
```
Hier werden die Ergebnisse der Abfrage durchlaufen. Jeder Suchbegriff, der die Kriterien erfüllt, wird in ein Array keywordsToExclude aufgenommen.

### Überprüfung und Erstellung der negativen Keyword-Liste
```javascript
// Name der negativen Keyword-Liste
var negativeListName = 'Keywords über 100 Impressionen ohne Klicks';

// Prüfen, ob die Liste bereits existiert
var negativeListIterator = AdsApp.negativeKeywordLists()
    .withCondition('Name = "' + negativeListName + '"')
    .get();

var negativeList;
if (negativeListIterator.hasNext()) {
  negativeList = negativeListIterator.next();
} else {
  // Erstellen einer neuen negativen Keyword-Liste, falls sie nicht existiert
  negativeList = AdsApp.newNegativeKeywordListBuilder()
      .withName(negativeListName)
      .build()
      .getResult();
}
```
In diesem Abschnitt wird überprüft, ob eine negative Keyword-Liste mit dem festgelegten Namen bereits existiert. Wenn nicht, wird eine neue Liste erstellt.

### Hinzufügen der Keywords als Exact Match
```javascript
// Hinzufügen der Keywords zur negativen Keyword-Liste als Exact Match
for (var i = 0; i < keywordsToExclude.length; i++) {
  negativeList.addNegativeKeyword('[' + keywordsToExclude[i] + ']');
}
```
Zum Schluss werden alle identifizierten Keywords als exakte Übereinstimmungen (Exact Match) zur negativen Keyword-Liste hinzugefügt. Die eckigen Klammern [ ] kennzeichnen dabei eine exakte Übereinstimmung.

## Zusammenfassung
Dieses Skript automatisiert den Prozess des Ausschlusses nicht effektiver Suchbegriffe in Google Ads, um die Effizienz von Werbekampagnen zu steigern. Es identifiziert Suchbegriffe mit hoher Sichtbarkeit, aber ohne Interaktion und schließt sie gezielt aus, um die Anzeigenrelevanz und CTR zu verbessern.

## Anwendung
Das Skript kann regelmäßig in Ihrem Google Ads-Konto ausgeführt werden, um die negative Keyword-Liste kontinuierlich zu aktualisieren. Es ist ratsam, die Liste periodisch zu überprüfen, um ihre Relevanz und Genauigkeit sicherzustellen.

## Anpassung
Das Skript kann modifiziert werden, um die Schwellenwerte zu ändern oder unterschiedliche Kriterien für den Ausschluss von Keywords anzuwenden. Es kann auch angepasst werden, um mit verschiedenen Kampagnentypen zu arbeiten oder mehrere Listen zu verwalten.

