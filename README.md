# SerienStream & Filmo IP für Cloudstream

Zwei getrennte Erweiterungen im selben Repository:

| Erweiterung | Inhalt | Version |
| --- | --- | --- |
| **SerienStream IP** | Serien von http://186.2.175.5/ | 3 |
| **Filmo IP** | Filme von http://45.10.243.23/ | 1 |

## Installieren

Diesen Repo-Link in Cloudstream unter **Einstellungen → Erweiterungen → Repository hinzufügen** eintragen:

https://raw.githubusercontent.com/aadel886/serienstream-ip/builds/repo.json

Ist das Repo schon vorhanden, einfach **aktualisieren** und zusätzlich
**Filmo IP** installieren. Auf der Cloudstream-Startseite anschließend die
gewünschte Quelle auswählen. Die aktuelle Cloudstream-Vorabversion wird benötigt.

## Filme auf dem Fire TV

Film suchen oder durch die Kategorien blättern, Film öffnen, Abspielen wählen,
dann Hoster und Sprache auswählen. Die Erweiterung übergibt den Stream an
Cloudstreams Player. VOE-Weiterleitungen und Byse-Zwischenseiten werden aufgelöst.
Bei den geprüften Filmquellen war kein CAPTCHA erforderlich.

Filmo IP bietet Kategorien, eine Filmübersicht mit weiteren Seiten, Suche,
Cover, Beschreibungen, Jahr, Laufzeit, Genres, Darsteller und Trailer,
soweit die Website diese Informationen liefert.

Die Quellenwahl zeigt die Qualitätsangabe der Website. Es gibt **kein 720p-Limit**
im Plugin: Alle vom Cloudstream-Extractor gelieferten Qualitätsstufen werden
übernommen. Eine 720p-Quelle erhält durch Hochskalieren keine echten 4K-Details.
Bei Quellen mit mehreren Tonspuren gegebenenfalls im Player Audio umstellen.

## Prüfstand

Beide Erweiterungen lassen sich kompilieren; Parser-, Freigabe-, Cookie-,
Redirect- und Repository-Tests laufen im GitHub-Workflow.
**Die vollständige Filmo-Wiedergabe und ein echtes Filmo-CAPTCHA wurden noch
nicht auf einem Android-/Fire-TV-Gerät getestet.** Die Film-Erweiterung ist
als Testversion gekennzeichnet. Die manuelle SerienStream-Freigabe bleibt bestehen.

## Quellcode und Updates

- **Source.zip:** SerienStream IP, mit Tests und eigener Anleitung.
- **FilmoSource.zip:** Filmo IP, mit Tests und eigener Anleitung.
- **.github/workflows/build.yml:** baut beide Archive und veröffentlicht
  `SerienStreamIP.cs3`, `FilmoIP.cs3`, `plugins.json` und `repo.json` im Branch `builds`.

Die Quelldateien liegen in den Archiven direkt im Hauptverzeichnis.
Versionsnummern stehen jeweils in `plugin.json`. Website-Dateien, Cookies,
Zugangsdaten und Videos gehören nicht in die Archive.
Build-Abhängigkeiten sind über SHA-256 festgelegt. Änderungen an Website oder
Hostern können eine neue Erweiterungs- oder Cloudstream-Version erfordern.
