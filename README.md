# PURUS Hausmeisterservice – Website

Statische Website (reines HTML/CSS), fertig zum Hochladen auf **GitHub Pages** und zur Verbindung mit deiner **Strato-Domain**. Kein Server, keine Datenbank, keine Build-Tools nötig – die fertigen Seiten liegen bereits im Ordner.

Schwerpunkt der Seite ist **Dachrinnenreinigung** (SEO-optimiert in Titeln, Hero, Navigation und Sitemap-Priorität), ergänzt um den kompletten Hausmeisterservice und 30 Ortsunterseiten.

---

## 1. Was ist enthalten

- **Startseite** mit Hero (Dachrinnenreinigung), Schwerpunkt-Band und dem PURUS-Kreis-Widget (Waschbär in der Mitte, 13 Leistungen im Kreis)
- **13 Leistungsseiten** unter `/leistungen/…/`
- **30 Ortsunterseiten** unter `/[leistung]/[ort]/` (6 Kernleistungen × Fürstenfeldbruck, Germering, Olching, Puchheim, Gröbenzell)
- **Einsatzorte-Übersicht**, **Über uns**, **Kontakt** (Formular), **Impressum**, **Datenschutz**, **Danke-Seite**, **404-Seite**
- **Schwebender „Kostenloses Angebot"-Button** + Schnellwahl-Button auf jeder Seite
- SEO-Technik: `sitemap.xml`, `robots.txt`, `canonical`, Open-Graph, **schema.org** (LocalBusiness, Service, FAQ, Breadcrumb), saubere URLs ohne `.html`
- `CNAME` (für die Domain) und `.nojekyll` (für GitHub Pages)

---

## 2. Lokal ansehen (optional)

Im Ordner einen kleinen Webserver starten:

```
python3 -m http.server 8000
```

Dann im Browser `http://localhost:8000` öffnen. (Direkt per Doppelklick auf `index.html` funktionieren die Links nicht, weil absolute Pfade wie `/assets/…` verwendet werden – deshalb der lokale Server.)

---

## 3. Auf GitHub hochladen & GitHub Pages aktivieren

1. Bei GitHub einloggen und ein **neues Repository** anlegen (z. B. `purus-website`), Sichtbarkeit **Public**.
2. Den **kompletten Inhalt dieses Ordners** ins Repository laden (per Web-Upload „Add file → Upload files", einfach alle Dateien und Ordner hineinziehen, oder per Git).
   - Wichtig: Die Dateien müssen im **Wurzelverzeichnis** liegen (also `index.html` direkt im Repo, nicht in einem Unterordner).
3. Im Repository auf **Settings → Pages** gehen.
4. Unter **Build and deployment → Source**: **„Deploy from a branch"** wählen, Branch **`main`**, Ordner **`/ (root)`**, dann **Save**.
5. Nach ein paar Minuten ist die Seite unter `https://<dein-benutzername>.github.io/purus-website/` erreichbar (Testadresse; die richtige Adresse folgt über die Domain in Schritt 4).

> Die Datei `.nojekyll` ist bereits enthalten – sie stellt sicher, dass GitHub die Seiten unverändert ausliefert.

---

## 4. Strato-Domain verbinden (www.purus-hausmeisterservice.de)

Im Repo liegt bereits eine Datei **`CNAME`** mit dem Inhalt `www.purus-hausmeisterservice.de`. Damit weiß GitHub, welche Domain gehört. Jetzt noch bei **Strato** die DNS-Einträge setzen:

**Bei Strato im Kundenbereich → Domainverwaltung → DNS-Einstellungen** deiner Domain:

**a) Für `www` (empfohlen als Hauptadresse) – CNAME-Eintrag:**

| Typ | Name/Host | Ziel/Wert |
|-----|-----------|-----------|
| CNAME | `www` | `<dein-benutzername>.github.io` |

(Nur der Benutzername + `.github.io`, **ohne** Repository-Namen.)

**b) Für die Domain ohne www (Apex `purus-hausmeisterservice.de`) – vier A-Records:**

| Typ | Name/Host | Wert |
|-----|-----------|------|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |

So leitet die Adresse ohne www ebenfalls auf die GitHub-Seite (GitHub leitet dann automatisch auf www weiter).

**c) Zurück bei GitHub → Settings → Pages:**
- Unter **Custom domain** `www.purus-hausmeisterservice.de` eintragen (falls nicht schon durch die `CNAME`-Datei gesetzt) und speichern.
- Nach erfolgreicher DNS-Prüfung den Haken bei **„Enforce HTTPS"** setzen (kann nach DNS-Umstellung einige Stunden dauern, bis er anklickbar ist).

> Hinweis: DNS-Änderungen bei Strato brauchen je nach Fall einige Minuten bis wenige Stunden, bis sie überall aktiv sind. Falls bei Strato bereits alte A-/CNAME-Einträge oder eine Weiterleitung für die Domain bestehen, diese vorher entfernen.

---

## 5. Kontaktformular aktivieren (E-Mail an info@purus-hausmeisterservice.de)

Das Formular auf `/kontakt/` nutzt **FormSubmit** – ein kostenloser Dienst, der die Formulardaten **ohne eigenen Server direkt per E-Mail** an eure Adresse schickt.

**Einmalige Aktivierung:**
1. Nach dem Livegang das Formular auf der Kontaktseite **einmal testweise absenden**.
2. FormSubmit schickt eine **Bestätigungs-E-Mail** an `info@purus-hausmeisterservice.de`.
3. In dieser Mail den **Bestätigungslink klicken** – danach kommen alle Anfragen automatisch in euer Postfach.

Das Formular leitet nach dem Absenden auf die **Danke-Seite** (`/danke/`) weiter.

> Optional (Spamschutz): FormSubmit bietet eine anonyme Endpoint-Variante mit einem Code statt der E-Mail-Adresse im Quelltext. Bei Bedarf im Formular in `kontakt/index.html` die Adresse in der `action` durch den FormSubmit-Code ersetzen (Anleitung auf formsubmit.co). Alternativ lässt sich auch ein anderer Anbieter (z. B. Formspree) eintragen.

---

## 6. Maskottchen (Waschbär) & Favicon einfügen

Damit im Kreis-Widget statt des Platzhalter-Schriftzugs „PURUS" euer Waschbär erscheint, legt zwei Bilder in den Ordner **`assets/img/`**:

- **`purus-maskottchen.png`** – die Waschbär-Grafik von der alten Seite (am besten als PNG mit transparentem Hintergrund)
- **`favicon.png`** – kleines Logo fürs Browser-Tab (z. B. 64×64 Pixel)

Solange die Dateien fehlen, zeigt die Seite den Schriftzug „PURUS" als sauberen Platzhalter – die Seite funktioniert also auch ohne die Bilder.

> Tipp: Ich kann euch den Waschbär und die Logos auf Wunsch von der alten Seite übernehmen und passend einbauen – einfach Bescheid geben.

---

## 7. Inhalte später ändern

Alle Seiten sind normale HTML-Dateien und lassen sich direkt bearbeiten. Wer viele Seiten auf einmal ändern will, nutzt den Generator (`build_site.py`) zusammen mit den Text-Dateien (Leistungstexte und Ortsunterseiten als Markdown). Sag einfach Bescheid, wenn ich Texte anpassen oder weitere Orte/Leistungen ergänzen soll.

---

## 8. Vor dem Livegang bitte prüfen (rechtlich)

- **Impressum:** Rechtsform (Einzelunternehmen/GbR) und die korrekte Schreibweise der USt-IdNr. ergänzen/prüfen.
- **Datenschutzerklärung:** Die enthaltene Vorlage rechtlich prüfen und an die tatsächlich genutzten Dienste anpassen (FormSubmit, Google Fonts, Bootstrap Icons, Hosting bei GitHub).
- **Google Fonts / Icons:** werden aktuell über ein CDN geladen. Für maximale DSGVO-Sicherheit können diese später lokal eingebunden werden (auf Wunsch mache ich das).

---

*Erstellt für PURUS Hausmeisterservice · Fürstenfeldbruck.*
