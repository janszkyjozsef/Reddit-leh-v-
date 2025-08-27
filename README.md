# Reddit Comment Exporter — Base Repo (ZIP-ready)

Cél: **Reddit kommentek letöltése 2012-től mostanáig**, teljes szöveggel, és **ZIP-be** csomagolása (CSV + DOCX + meta + README).
Ingyenes hivatalos Reddit API-t használ (`client_id` + `client_secret` + OAuth token).

## 0) Reddit app létrehozása (képernyőfotó rublikáihoz pontos értékek)
Menj: https://www.reddit.com/prefs/apps → **create another app…**

**Töltsd a mezőket így (copy‑paste kész):**
- **name**: `Reddit Comment Exporter (Local)`
- **type**: `script`  (személyes, helyi futtatáshoz)
- **description**: `Local tool to export subreddit comments for research (read-only).`
- **about url**: `https://github.com/your-username/reddit-comment-exporter`
- **redirect uri**: `http://localhost:8080`
- pipálj be egy friss reCAPTCHA-t, majd **create app**.

Létrejön egy blokk, benne: **personal use script** alatt a **client_id**, és alatta a **client secret**.

> Tipp: Ha nem akarsz secrettel bajlódni, a `type: installed` is jó, ilyenkor a secret üres, a kód pedig az `installed_client` grantet használja.

## 1) .env kitöltése
Másold `.env.example` → `.env`, majd töltsd ki:
```
CLIENT_ID=xxx
CLIENT_SECRET=yyy            # ha installed app, hagyd üresen
USER_AGENT=linux:joci-reddit-scraper:1.0 (by /u/YOUR_REDDIT_USERNAME)
```

## 2) Telepítés
```bash
pip install -r requirements.txt
```

## 3) Futás (példa)
```bash
python run_export.py --subreddit epilepsy --from 2012-01-01 --to now --query ""
```
Kimenet: `exports/reddit_comments_<sub>_<YYYYMMDD_HHMMSS>.zip`  
A ZIP-ben: `.csv`, `.docx`, `_meta.json`, `_README.txt`.

## 4) Paraméterek
- `--subreddit` (kötelező, pl. `AskScience` vagy `epilepsy`)
- `--query` (opcionális, üres = minden)
- `--from` ISO dátum (alap: 2012-01-01)
- `--to` ISO dátum vagy `now` (alap: now)

## 5) Jog és limit
- Egyedi **User-Agent** kötelező. Ne tedd nyilvános repo‑ba a secretet.
- Rate‑limit esetén a script **vár**, majd folytatja.
- Csak nyilvános tartalmat húz le; törölt/eltávolított kommentet az API nem ad vissza.
