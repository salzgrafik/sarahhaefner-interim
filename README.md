# Platzhalterseite sarahhaefner.de

Statische Übergangsseite, bis der Rebuild (`../sarahhaefner-rebuild/`) live geht.
Kein Build-Tool, kein JavaScript, keine externen Requests. Alle Pfade relativ.

## Inhalt

```
platzhalter/
├── index.html              Coming-Soon-Seite
├── 404.html                Fehlerseite (inline CSS, keine Abhängigkeiten)
├── impress/index.html      Impressum (Original-Wortlaut)
├── privacy-policy/index.html  Datenschutzerklärung (Original-Wortlaut)
├── css/style.css
├── fonts/                  Fraunces (variable) + Inter Tight 500, self-hosted
└── .nojekyll               verhindert Jekyll-Verarbeitung auf GitHub Pages
```

Gesamtgröße ohne Fonts: ~40 KB. Mit Fonts: ~185 KB.

## Deploy auf GitHub Pages

Git-Repo ist bereits initialisiert, erster Commit liegt vor (Branch `master`).

1. Repo auf GitHub anlegen (z. B. `sarahhaefner-platzhalter`, public — Pages braucht bei Free-Accounts ein öffentliches Repo).
2. Lokal im Ordner `platzhalter/`:

   ```bash
   rm -f .git/*.lock .git/refs/heads/*.lock
   find .git/objects -name 'tmp_obj*' -delete
   git branch -M main
   git remote add origin git@github.com:<user>/sarahhaefner-platzhalter.git
   git push -u origin main
   ```

3. Auf GitHub: **Settings → Pages → Source: Deploy from a branch → main / (root)** → Save.
4. Nach ein paar Minuten läuft die Seite unter `https://<user>.github.io/sarahhaefner-platzhalter/`.

## Custom Domain sarahhaefner.de

Erst wenn die Seite unter der github.io-Adresse geprüft ist:

1. Datei `CNAME` im Repo-Root anlegen, Inhalt: `www.sarahhaefner.de`
   (oder über Settings → Pages → Custom domain eintragen, GitHub legt sie selbst an)
2. DNS bei All-inkl (kas.all-inkl.com → Domain → sarahhaefner.de → DNS-Einstellungen):
   - `CNAME` für `www` → `<user>.github.io`
   - `A`-Records für `@` (Apex) auf die vier GitHub-IPs:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - Alte Webflow-Records entfernen
3. In Settings → Pages **Enforce HTTPS** aktivieren, sobald das Zertifikat ausgestellt ist (kann bis zu 24 h dauern).

**Achtung:** Sobald das DNS umgestellt ist, ist die Webflow-Seite nicht mehr erreichbar. Vorher prüfen, ob die Platzhalterseite steht.

## Lokal ansehen

```bash
cd platzhalter
python3 -m http.server 8000
# → http://localhost:8000
```
