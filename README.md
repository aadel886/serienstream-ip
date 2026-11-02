# SerienStream IP für Cloudstream

Experimentelle Erweiterung für http://186.2.175.5/ mit Serienkategorien, Suche,
Cover, Beschreibungen, Staffeln/Episoden und manueller CAPTCHA-Freigabe.
Version 2 enthält eine Fernbedienungsleiste für Android TV / Fire TV.

## Installation

Repo-Link in Cloudstream unter **Einstellungen → Erweiterungen → Repository hinzufügen** eintragen:

https://raw.githubusercontent.com/aadel886/serienstream-ip/builds/repo.json

Danach **SerienStream IP** installieren. Die aktuelle Cloudstream-Vorabversion
wird benötigt. Die Installationsdateien entstehen nach dem ersten erfolgreichen
GitHub-Actions-Lauf im Branch `builds`.

## Teststatus

Kompilierung, Android-DEX und Parser-Tests mit aktuellen Website-Seiten bestanden.
**Wiedergabe und CAPTCHA noch nicht auf einem echten Android-/Fire-TV-Gerät getestet.**
Das CAPTCHA wird von dir selbst bestätigt; je nach Website und WebView kann eine
Maus erforderlich sein. Videoqualität und Sprachen hängen vom Hoster ab.

Fire OS 6+ erfüllt die Android-Mindestversion. Vega OS unterstützt diese
Android-Erweiterung nicht. Ein Fire TV Stick 4K Plus nutzt Fire OS 8.

## Quellcode und Updates

Der komplette Quellcode samt Tests, Abhängigkeiten und ausführlicher Anleitung
liegt in **Source.zip**. Zum Bearbeiten entpacken, Änderungen vornehmen,
`version` in `plugin.json` erhöhen und das aktualisierte Source.zip hochladen.
Der Workflow entpackt das Archiv, kompiliert den Code, führt die Parser-Tests aus
und veröffentlicht das Plugin im Branch `builds`.

Die Quelldateien müssen im Archiv direkt im Hauptverzeichnis liegen.
Build-Abhängigkeiten sind mit SHA-256 festgelegt. Ändert sich die offizielle
Cloudstream-API-Datei, stoppt ein frischer Build bis zur geprüften Aktualisierung
von `dependencies.json`. Änderungen der Website werden nicht automatisch repariert.

Referenzen: [Cloudstream-TV-Anleitung](https://recloudstream.github.io/csdocs/other-devices/tv/),
[Amazon Fire OS](https://developer.amazon.com/docs/fire-tv/fire-os-overview.html).
