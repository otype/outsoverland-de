<div align="center">

# ↪️ outsoverland-de

**Leitet `outsoverland.de` auf `outsoverland.com` weiter, Pfad inklusive.**

[![Letzter Commit](https://img.shields.io/github/last-commit/otype/outsoverland-de/main?style=flat-square&logo=github&logoColor=white)](https://github.com/otype/outsoverland-de/commits/main)
[![Ziel](https://img.shields.io/badge/Ziel-outsoverland.com-4a7c59?style=flat-square)](https://outsoverland.com)

</div>

---

Eine winzige GitHub-Pages-Seite ohne Build-Schritt. Sie hängt an der Domain `outsoverland.de` (und `www.outsoverland.de`) und schickt Besucher auf [outsoverland.com](https://outsoverland.com) weiter. Die eigentliche Website liegt in [`otype/outsoverland-site`](https://github.com/otype/outsoverland-site).

## 🧩 Warum ein eigenes Repo?

GitHub Pages erlaubt pro Repository genau **eine** eigene Domain. Die Website selbst läuft unter `outsoverland.com`, also braucht `outsoverland.de` ein eigenes Repository, das nichts weiter tut, als weiterzuleiten.

## 🔀 So funktioniert die Weiterleitung

| Aufruf | Ergebnis |
| --- | --- |
| `outsoverland.de/` | `outsoverland.com/` |
| `outsoverland.de/de/` | `outsoverland.com/de/` (Pfad, Query und Anker bleiben erhalten) |
| `www.outsoverland.de/…` | GitHub leitet auf `outsoverland.de/…` um, dann geht es wie oben weiter |
| unbekannter Pfad | GitHub liefert `404.html`, und die leitet genauso weiter |

Die Weiterleitung passiert im Browser und ist **keine HTTP-301-Weiterleitung**:

- **Mit JavaScript:** `location.replace('https://outsoverland.com' + pathname + search + hash)` öffnet denselben Pfad auf `.com`.
- **Ohne JavaScript:** ein `<meta http-equiv="refresh">` führt auf die Startseite von `outsoverland.com`.
- Die Seite trägt `noindex` und einen `canonical`-Link auf `outsoverland.com/`, damit Suchmaschinen die `.de`-Adresse nicht als eigene Seite führen.

## 📁 Dateien

| Datei | Zweck |
| --- | --- |
| `index.html` | die Weiterleitung (Startseite der Domain) |
| `404.html` | **identische Kopie** von `index.html`, damit auch Unterseiten weiterleiten |
| `CNAME` | die eigene Domain: `outsoverland.de` |
| `.nojekyll` | schaltet Jekyll ab, die Dateien werden unverändert ausgeliefert |

## ✏️ Ändern

`index.html` und `404.html` müssen **gleich bleiben**. Nach einer Änderung also kopieren und prüfen:

```console
$ cp index.html 404.html
$ diff -q index.html 404.html && echo identisch
```

Ein Push auf `main` veröffentlicht die Seite (Pages-Quelle: Branch `main`, Wurzelverzeichnis). Danach prüfen:

```console
$ curl -s -o /dev/null -w '%{http_code}\n' https://outsoverland.de/
```

## 🌐 DNS

Die Domain `outsoverland.de` zeigt auf GitHub Pages. `www` ist ein `CNAME` auf `otype.github.io.`, die Apex-Einträge entsprechen denen von `outsoverland.com` (siehe [DNS-Abschnitt der Website](https://github.com/otype/outsoverland-site#-domains)). Unter Settings → Pages sind die eigene Domain `outsoverland.de` und **Enforce HTTPS** eingestellt.
