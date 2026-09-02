# `manifest.json` — Messstand aus Auftrag A1 (Punkt 146)

Dies ist **nicht** die endgültige Adresse des Manifests.

Auftrag A1 verlangt das Manifest **hinter einer eigenen Domäne**, gerade
*nicht* hinter der Adresse des Anbieters — sonst kostet ein
Anbieterwechsel eine App-Auslieferung. Diese Datei liegt hier aus einem
einzigen Grund: damit sich messen lässt, dass ein Klient sie wirklich
abrufen und gegen die Auslieferung prüfen kann.

* Erzeugt von `cloud/manifest_bauen.py` im Repo `Waytide` (Zweig `extern/A1`).
* Geprüft von `cloud/manifest_pruefen.py` — gegen die Dateien, gegen den
  Rust-Leser und gegen die laufende Auslieferung.
* Beschreibt den Kachelstand `3a7e19e55ceb22ab154829f056d0afbdcb74b065`
  dieses Repos: 2 Kacheln, 48 nichtleere 1°-Blöcke, 432.979.994 Byte.

Die Kacheln selbst liegen unverändert in `main` bzw. unter dem oben
genannten Commit; diese Datei fügt ihnen nichts hinzu und nimmt ihnen
nichts weg.
