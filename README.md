# Michael Carpenter: portfolio site

Hey Andrew,

This is your portfolio site, and from here on it's yours. Uncle Matt had it built for you as a starting point. The look is a game-dev terminal: a phosphor-green HUD, matrix rain, a "Press start" button and a "Continue?" countdown at the bottom. The bones are solid. What it needs now is **your** work: real titles, real stills, real video.

You've shipped on GTA VI, so this will be easy for you. It's one HTML file with no framework, no build step and no website builder. You own every pixel.

Right now it lives at **https://mattcarpenter.com/michael-carpenter/**. Once you've set it up (below), it'll live at your own address.

---

## 0. Taking it over (about 10 minutes, once)

### a. Get the repo

Uncle Matt will transfer this repo to your GitHub account. You'll get an email from GitHub, and you just click **Accept**. No GitHub account yet? Make one at https://github.com/signup. It's free.

### b. Make it public

GitHub Pages hosts sites for free from **public** repos. Go to **Settings → General**, scroll to the **Danger Zone**, click **Change visibility**, and choose **Public**. Nothing in here is secret.

### c. Pick your URL

You have two good options:

| Option | Your site's address | How |
|---|---|---|
| **Free, clean** | `https://YOUR-USERNAME.github.io/` | Rename the repo to exactly `YOUR-USERNAME.github.io` (**Settings → General → Repository name**). |
| **Your own domain** | `https://michaelcarpenter.xyz` (whatever you buy) | Do the rename above, then follow section 8. A domain costs roughly $10–20 a year. |

If you skip the rename, the site still works, just at the uglier `https://YOUR-USERNAME.github.io/mc-michael-carpenter-site/`.

### d. Turn on GitHub Pages

1. Go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Set **Branch** to `main`, set the folder to `/ (root)`, and click **Save**.
4. Wait about a minute and refresh. GitHub shows your live URL at the top of that page.

From then on, **every push to `main` updates the live site automatically**, usually within a minute.

### e. Tell Uncle Matt the new URL

He'll point `mattcarpenter.com/michael-carpenter/` at your site so old links keep working.

### f. About the Webflow site

The site at `michael-carpenter-portfolio.webflow.io` is separate. Nothing here depends on it, so keep it or cancel it as you like.

---

## Two ways to edit

**In the browser, no setup.** Open `index.html` on GitHub, click the pencil icon, edit, then click **Commit changes**. For images, open the `img/` folder and use **Add file → Upload files**. This is fine for text tweaks and swapping media.

**On your machine, better for real work.** Clone the repo, open the folder in VS Code (or anything), and open `index.html` in a browser. Edit, save and refresh. When you're happy:

```zsh
git add -A && git commit -m "Real titles and poster frames" && git push
```

Anything in **[square brackets]** in `index.html` is a placeholder for you to replace. Search the file for `[` to find them all.

---

## 1. Text placeholders

| What | Where in `index.html` | Example |
|---|---|---|
| Piece titles | The four `<h3>[Title of piece 0X]</h3>` lines in the **Cartridges** section | `<h3>Neon Drift</h3>` |
| Discipline and year | The `<div class="meta">` line above each title | `<span>Level design</span><span>2025</span>` |
| One-line description | The `<p>` under each title | About one sentence: the idea, and what *you* did on it. |
| Player card | `[City]`, `[Unreal · Maya · Resolve]` and `LV. [—]` | Your real city and tools. The level could be years in the industry. |
| Email | `<code>[email@domain]</code>` near the bottom | `<code>you@example.com</code>` |
| Social links | The `href="#continue"` links for `[itch.io]`, `[LinkedIn]` and `[CV]` | `<a href="https://www.linkedin.com/in/you">LinkedIn ↗</a>` |
| Headline | The `<p class="pitch">` line | Rewrite it in your own words. |
| Quest log | The three `<article class="quest">` blocks | Describe how you actually work. |
| Page title | `<title>` and `<meta name="description">` at the top | This is what shows in Google and in link previews. |

**Credits.** If you're allowed to name shipped titles (GTA VI and anything else), say so. A studio name on a portfolio is worth more than any animation on the page. Check your NDA first on what you can show versus what you can only name.

**Level Select table.** Its rows come from the `pieces` list in the `<script>` near the bottom, not from the HTML. Edit each line there:

```js
{ no:'01', t:'Neon Drift', ty:'Level design', f:'16:9 · 24 fps', s:48, y:'2025', h:'https://vimeo.com/1189991940' },
```

- `t` is the title and `ty` is the type.
- `f` is the format.
- `s` is the runtime in seconds. It sets the bar length, and the longest piece is scaled to 48s.
- `y` is the year and `h` is the link.

Keep the titles here matching the ones on the cards.

---

## 2. Images (poster frames)

Each card currently shows a small animated placeholder scene drawn on a `<canvas>`. To show a real still instead:

1. Export a frame from your edit at **1920×1080** (16:9). Save it as JPG or WebP and keep it under about 300 KB.
2. Put it in the `img/` folder, for example `img/piece-01.jpg`.
3. In that card, replace the `<canvas ...></canvas>` with an image:

```html
<!-- before -->
<div class="screen"><canvas data-scene="terrain" aria-hidden="true"></canvas> ...
<!-- after -->
<div class="screen"><img src="img/piece-01.jpg" alt="Neon Drift, night race through the city"> ...
```

4. Delete the `<span class="chip pf">[poster frame]</span>` label on that card.

The CSS already crops images to fill the frame. The page skips the animation for any card that has no canvas, so you can swap them one at a time.

---

## 3. Moving video on the cards (optional)

For a silent looping preview instead of a still, use a Vimeo **background** embed in place of the canvas:

```html
<div class="screen">
  <iframe src="https://player.vimeo.com/video/1189991940?background=1&autoplay=1&loop=1&muted=1"
          title="Neon Drift preview" allow="autoplay; fullscreen" loading="lazy"></iframe>
  ...
</div>
```

Swap in each video's ID: the number at the end of its `vimeo.com/...` link.

The card stays clickable because the CSS makes the video ignore clicks, so a click still opens the full video on Vimeo. Four autoplaying videos is heavy on phones, though. A good compromise is video on the first card and stills on the rest.

A self-hosted MP4 also works:

```html
<video src="img/piece-01-loop.mp4" autoplay muted loop playsinline></video>
```

Keep the MP4 short (5 to 10 seconds) and small (under about 4 MB). GitHub rejects files over 100 MB, and big files make the page slow anyway. Put long videos on Vimeo.

---

## 4. The reel banner at the top

The wide banner is 5:1, which matches your 1920×384 reels. To play the real reel in it, replace

```html
<canvas id="reelfx" aria-hidden="true"></canvas>
```

with

```html
<iframe src="https://player.vimeo.com/video/1190864100?background=1&autoplay=1&loop=1&muted=1"
        title="Film, Television & Gaming Reel" allow="autoplay; fullscreen"></iframe>
```

The page runs fine without the canvas.

The timecode in the bottom bar is decorative and counts 0 to 20 seconds. If it drifts out of sync with the real reel and bugs you, delete the `<div class="reel-bot">` line.

---

## 5. Adding or removing a piece

- **Add a piece:** copy a whole `<a class="tile">…</a>` block, change its number, text, image and link, and add a matching line to `pieces`.
- **Remove a piece:** delete its block and its line in `pieces`.
- Update the count in `<span class="label">4 pieces · 1080p · 24 fps</span>` so it matches.

The grid is two columns on desktop and one on phones. An even number of pieces looks best on desktop.

---

## 6. Colours, fonts, icon

All colours are defined at the top of the `<style>` block:

```css
--phos:#6CFFB0;   /* the green accent */
--hot:#FF4D6D;    /* the red REC dot and glitch */
--void:#050807;   /* background */
```

Change `--phos` to change the accent everywhere. The fonts are **Tektur** (display) and **JetBrains Mono** (everything else), both from Google Fonts.

The browser-tab icon is `favicon.svg`, a green "MC". Edit it or replace it.

---

## 7. Letting Google find you

The page currently tells search engines to stay away, because it's full of placeholders. When the real content is in, delete this line near the top of `index.html`:

```html
<meta name="robots" content="noindex,nofollow">
```

---

## 8. Using your own domain (optional)

1. Buy a domain from any registrar (Cloudflare, Namecheap, Porkbun and others).
2. In the repo, go to **Settings → Pages → Custom domain**, enter it (for example `michaelcarpenter.xyz`), and click **Save**. GitHub adds a `CNAME` file to the repo for you.
3. At your registrar, add these DNS records:

   | Type | Name | Value |
   |---|---|---|
   | A | `@` | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |
   | CNAME | `www` | `YOUR-USERNAME.github.io` |

4. Wait for DNS to propagate (usually minutes, sometimes a few hours). Then tick **Enforce HTTPS** on the same Pages settings screen.

---

## Checklist

- [ ] Accept the transfer, make the repo public, rename it to `YOUR-USERNAME.github.io`
- [ ] Turn on GitHub Pages and send Uncle Matt the URL
- [ ] Replace every `[bracket]` (search for `[`)
- [ ] Real poster frames in `img/`, and the real reel in the banner
- [ ] Email, LinkedIn, CV and itch.io links
- [ ] Remove the `noindex` line
- [ ] (Optional) your own domain

Go make it yours. And if you break something, `git log` remembers everything, so nothing is ever really lost.

Proud of you, kid.

— Uncle Matt
