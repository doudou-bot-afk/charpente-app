[README.md](https://github.com/user-attachments/files/33627606/README.md)
# charpente-app# Charpente — Telegram Mini App

A French conjugation drill (présent, imparfait, passé composé, plus-que-parfait, futur)
that runs inside Telegram. It is a single file, `index.html`, with no build step and no server code.

## What it does inside Telegram

- Opens full-screen and follows the user's Telegram light/dark theme
- Telegram's own **Back** button returns to the tense menu
- Haptic feedback on correct and wrong answers
- Greets the user by first name
- Saves progress per tense in Telegram **CloudStorage**, so it syncs across the user's phone and desktop.
  In a normal browser it falls back to `localStorage`.

## 1. Put it online (HTTPS is required)

Telegram only opens Mini Apps from an `https://` URL. The easiest free option is GitHub Pages:

1. Create a public repository on GitHub, e.g. `charpente-app`.
2. Upload `index.html` to it (**Add file → Upload files**).
3. **Settings → Pages →** Source: *Deploy from a branch*, branch `main`, folder `/ (root)` → **Save**.
4. After about a minute the app is live at `https://<your-username>.github.io/charpente-app/`.

Netlify Drop (drag the folder onto app.netlify.com/drop) or Vercel work just as well.

## 2. Create the bot and attach the app (@BotFather)

In Telegram, open **@BotFather**:

1. `/newbot` → choose a name and a username ending in `bot` (e.g. `CharpenteBot`).
2. Add a menu button that opens the app:
   `/mybots` → your bot → **Bot Settings → Menu Button → Configure menu button** →
   send the URL from step 1 → send a title, e.g. `Exercices`.
3. Optional, for a direct link like `t.me/CharpenteBot/app`:
   `/newapp` → pick the bot → title, description, a 640×360 image → the URL → a short name (`app`).
4. Optional, so the app opens from the bot's profile: `/mybots` → your bot → **Bot Settings → Configure Mini App → Enable Mini App** → the URL.

Open your bot and tap the menu button. The app should start.

## 3. Updating

Edit `index.html`, upload it again to the repository, and GitHub Pages republishes it in about a minute.
Telegram may cache the page, so fully close and reopen the app to see changes.

## Editing exercises

All exercises are in the `EX` array in `index.html`:

```js
{k:"ÊTRE · PRÉSENT DE L'INDICATIF", q:'Je ___ étudiant.', a:'suis'},
{k:"ÊTRE · PRÉSENT DE L'INDICATIF", type:'choice', q:'___ un film magnifique.', a:"C'est", c:["C'est","Ce sont"]},
```

- `k` is `VERB · TENSE`. The part after ` · ` decides which tense menu entry the exercise appears in,
  so a new tense (e.g. `CONDITIONNEL PRÉSENT`) gets its own entry automatically.
- `q` is the sentence, with `___` marking the blank.
- `a` is the answer. Typed answers ignore case and accents, so `etait` counts as `était`.

## Testing in a browser

Open `index.html` directly, or serve the folder (`python -m http.server`) and open it in the browser.
Outside Telegram it shows an in-page back arrow instead of Telegram's own, and has no haptics.
