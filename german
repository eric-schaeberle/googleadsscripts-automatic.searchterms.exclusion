* @Email: eric.schaeberle@skaleup.de
* @Autor: Eric Schäberle
* @github-slug: googleadsscripts-automatic.searchterms.exclusion
*
* Dieses Google Ads-Skript identifiziert automatisch Suchbegriffe mit über
* 100 Impressionen und keinen Klicks und fügt sie als exakte Übereinstimmungs-
* negative Schlüsselwörter zu einer bestimmten Liste hinzu, um die Werbeausgaben
* zu optimieren.
*/


function main() {
  // Abfrage, um Suchbegriffe mit mindestens 100 Impressionen und keinen Klicks zu finden
  const report = AdsApp.report(
      `SELECT search_term_view.search_term, ` +
      `metrics.impressions, metrics.clicks ` +
      `FROM search_term_view ` +
      `WHERE metrics.impressions >= 100 ` +
      `AND metrics.clicks = 0`);

  const rows = report.rows();
  const keywordsToExclude = [];

  // Sammeln der Suchbegriffe
  while (rows.hasNext()) {
    var row = rows.next();
    var keywordQuery = row['search_term_view.search_term'];
    keywordsToExclude.push(keywordQuery);
  }

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

  // Hinzufügen der Keywords zur negativen Keyword-Liste als Exact Match
  for (var i = 0; i < keywordsToExclude.length; i++) {
    negativeList.addNegativeKeyword('[' + keywordsToExclude[i] + ']');
  }
}
