# SerienStream IP für Cloudstream — Version 3

Experimentelle Android-Erweiterung für **http://186.2.175.5/**.
Serienkategorien, Suche, Cover, Beschreibungen, Staffeln und Episoden werden
in Cloudstreams eigener Oberfläche angezeigt.

## Installieren oder aktualisieren

Repository-Adresse:

https://raw.githubusercontent.com/aadel886/serienstream-ip/builds/repo.json

In Cloudstream unter **Einstellungen → Erweiterungen** dieses Repository
hinzufügen und **SerienStream IP** installieren. Ist es bereits installiert,
das Repository aktualisieren, das Plugin auf **Version 3** aktualisieren und
Cloudstream vollständig schließen und erneut öffnen. Kein neues Repository nötig.
Je nach App-Version heißen die Schaltflächen etwas anders.

Die Erweiterung wurde gegen die aktuelle Cloudstream-Vorabversion gebaut.
Android API 23 oder neuer wird benötigt; der Fire TV Stick 4K Plus mit Fire OS 8
erfüllt diese Voraussetzung. Eine aktuelle Android-System-WebView ist für
Cloudflares CAPTCHA wichtig.

## Folge abspielen

1. In Cloudstream die Quelle **SerienStream IP** öffnen und eine Folge auswählen.
2. Im nativen Dialog Hoster und Sprache wählen, z. B. **VOE [Deutsch]**.
3. Falls erforderlich, im kompakten Fenster das CAPTCHA selbst bestätigen.
   Eine erfolgreiche Bestätigung sendet das normale Freigabeformular automatisch ab.
4. Nach der Weiterleitung schließt das Fenster. Der Hoster-Extractor liefert
   die verfügbaren Streams an Cloudstreams Player. In dessen Quellenliste
   stehen Hoster, Sprache und die vom Extractor gelieferten Varianten.

Es wird jeweils die zuvor ausgewählte Hoster-/Sprachkombination aufgelöst.
Es gibt keine Zusage, dass alle Sprachen gleichzeitig ohne weitere Freigabe
in der Quellenliste verfügbar sind. Qualität, Untertitel und Tonspuren hängen
vom Hoster ab; 4K wird nicht garantiert.

Mit **Zum CAPTCHA** wechselt der Fokus in die Freigabe. Die **Menütaste** führt
zur Bedienleiste zurück. **Erneut versuchen** lädt eine frische Sitzung und ein
neues Formular; **Abbrechen** oder **Zurück** beendet den Vorgang.
Die CAPTCHA-Oberfläche stammt von Cloudflare. Abhängig von WebView und
Fernbedienung kann für das Kästchen weiterhin eine Maus nötig sein.
Es gibt keine automatische CAPTCHA-Lösung und keine Zugangsdaten im Plugin.

## Änderung gegenüber Version 2

Version 2 konnte den Hoster im eingebetteten Browser laden, ohne die Adresse
an Cloudstream zu übergeben. Androids Request-Callback meldet bei
Weiterleitungen nur die ursprüngliche URL; wechselnde Hoster-Domains konnten
zusätzlich an der bisherigen Domainliste scheitern.

Version 3 verwendet:

- Eine native Quellen- und Sprachauswahl vor der Freigabe.
- Ein eigenes kompaktes Formular am ursprünglichen Website-Ursprung mit
  aktuellen Website-Tokens, denselben Sitzungs-Cookies und demselben User-Agent
  wie die WebView. Das Formular nutzt die reguläre Turnstile-Prüfung der Website.
- Eine Formular-Weiterleitung im Hauptfenster statt in einem Video-Iframe.
  Die externe Zieladresse wird abgefangen; im Fenster ist kein Video-Player eingebaut.
- Normale GET-Weiterleitungen für bereits freigegebene Sitzungen, ohne erneut
  ein CAPTCHA zu verlangen, sofern die Website das erlaubt.
- Hoster-Auswahl anhand des von der Website gelieferten Namens, damit z. B.
  neue VOE-Mirror-Domains an den vorhandenen VOE-Extractor übergeben werden.
- Benannte Quellen im Cloudstream-Player sowie sichtbare Fehler- und Wiederholungsaktionen.

Die vorhandenen Cloudstream-Extractoren bleiben für die eigentlichen Videolinks
zuständig. Wenn ein Hoster seine Technik ändert, kann ein Cloudstream-Update
oder eine weitere Anpassung erforderlich sein.

## Prüfstand und Grenzen

Am **2. November 2026** bestanden:

- Kotlin-Kompilierung, Android-DEX-Erzeugung und CS3-Paketprüfung.
- Parser-Regressionsprüfungen für Serien, Bilder, Specials und Episoden.
- Tests mit einem lokalen HTTP-Server für Cookies, relative Weiterleitungen,
  neue Hoster-Domains, Fehlerantworten und Weiterleitungsschleifen.
- Tests für frische Freigabe-Tokens, die ausgewählte Sprache, Formular-Escaping
  und die Weiterleitung im Hauptfenster.
- JavaScript-Tests mit einer simulierten Turnstile-API: keine Übermittlung vor
  Bestätigung, automatische Übergabe danach, keine doppelten Übermittlungen,
  abgelaufene Freigaben und Fehlermeldungen.
- Prüfung der Formularstruktur anhand einer aktuellen öffentlichen Episodenseite
  mit zwei Quellen. Dabei wurde kein echtes CAPTCHA abgeschickt.

**Offen: CAPTCHA und vollständige Wiedergabe auf einem echten Android-/Fire-TV-Gerät.**
Ein erfolgreicher Build ist kein Beleg für erfolgreiche Wiedergabe. Diese Version
ist ein gezielter Reparaturversuch für die beobachtete Übergabestörung.
Wenn es weiterhin scheitert, helfen Cloudstream-Version, Plugin-Version,
Serie/Folge, gewählte Sprache und der genaue Text der Fehlermeldung.
Keine Passwörter, Cookies oder Freigabe-Tokens weitergeben.

Favoriten, Verlauf, Pause und Spulen gehören zur Cloudstream-App.

## Quellcode und Build

Im veröffentlichten GitHub-Repository liegt der vollständige Quellcode in
**Source.zip**, mit den Quelldateien direkt im Archiv-Hauptverzeichnis.
Der Workflow im Repository entpackt dieses Archiv, führt die Tests aus und
veröffentlicht `SerienStreamIP.cs3`, `plugins.json` und `repo.json` im Branch `builds`.

Zum lokalen Bauen Source.zip entpacken. Voraussetzungen:
**Python 3.10+, Java 17+, Node.js 18+** und Internetzugang für die Build-Abhängigkeiten.
Ein vollständiges Android-SDK wird nicht benötigt.

```bash
python tools/build.py --repo aadel886/serienstream-ip
```

Optional eine lokal gespeicherte aktuelle Episodenseite prüfen:

```bash
python tools/build.py --repo aadel886/serienstream-ip --episode-fixture /pfad/episode.html
```

Ausgaben liegen in `dist/`, der Testbericht in `build/build-report.json`.
Website-Seiten, Sitzungen und Freigabe-Tokens gehören nicht in das Quellarchiv.
Für Updates `version` in `plugin.json` erhöhen und das aktualisierte Source.zip
hochladen. Das Archiv enthält auch einen alternativen Workflow für Repositories,
die den entpackten Quellcode direkt im Hauptverzeichnis verwalten.

Downloads sind über SHA-256 in `dependencies.json` festgelegt. Bei einer geänderten
Cloudstream-API-Datei stoppt der Build, bis Kompatibilität und Prüfsumme überprüft
wurden. Änderungen an Website und Hostern werden nicht automatisch repariert.

## Technische Referenzen

- [Cloudstream-API und Extractoren](https://github.com/recloudstream/cloudstream)
- [Offene AniWorld-/SerienStream-Implementierungen zum Vergleich](https://github.com/Bnyro/GermanProviders)
- [Vom Nutzer genanntes Phisher-Repository](https://github.com/phisher98/cloudstream-extensions-phisher):
  dessen AniWorld-Paket beschreibt auch SerienStream mit Anmeldung in den
  Erweiterungs-Einstellungen. Der aktuelle Hauptbranch enthält keinen entsprechenden
  offenen Provider-Quellcode; dieser Fix behauptet nicht, dessen Implementierung zu kopieren.
- [Android: WebViewClient und Redirect-Callbacks](https://developer.android.com/reference/android/webkit/WebViewClient)
- [Cloudflare: Turnstile in WebViews](https://developers.cloudflare.com/turnstile/get-started/mobile-implementation/)
- [Cloudstream auf TV-Geräten](https://recloudstream.github.io/csdocs/other-devices/tv/)

Build-Abhängigkeiten unterliegen ihren jeweiligen Lizenzen. Die Erweiterung
enthält weder Website-Inhalte noch Videos.
