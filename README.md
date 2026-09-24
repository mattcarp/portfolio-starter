# mc-michael-carpenter-site

Hey Andrew, this is your portfolio site. It's live at **https://mattcarpenter.com/michael-carpenter/**.

The whole site is one file, `index.html`: plain HTML, CSS and a bit of JavaScript, with no build step and no framework. To preview it, open `index.html` in a browser. Edit it in any code editor (VS Code is a good choice) and refresh the page to see your changes.

Anything in **[square brackets]** is a placeholder for you to replace. Search the file for `[` to find them all.

---

## 1. Text placeholders

| What | Where in `index.html` | Example |
|---|---|---|
| Piece titles | The four `<h3>[Title of piece 0X]</h3>` lines in the **Cartridges** section | `<h3>Neon Drift</h3>` |
| Discipline and year | The `<div class="meta">` line above each title | `<span>Level design</span><span>2025</span>` |
| One-line description | The `<p>` under each title | Keep it to about one sentence. |
| Player card | `[City]` and `[Unreal · Maya · Resolve]` next to **Base** and **Loadout** | Your real city and tools |
| Email | `<code>[email@domain]</code>` near the bottom | `<code>you@example.com</code>` |
| Social links | The `href="#continue"` links for `[itch.io]`, `[LinkedIn]` and `[CV]` | `<a href="https://yourname.itch.io">itch.io ↗</a>` |
| Headline | The `<p class="pitch">` line | Rewrite it in your own words. |
| Quest log | The three `<article class="quest">` blocks | Describe your real process. |

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

1. Export a frame from your edit (or take a screenshot) at **1920×1080** (16:9). Save it as JPG or WebP and keep it under about 300 KB.
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

The card stays clickable because the CSS makes the video ignore clicks, so a click still opens the full video on Vimeo. Four autoplaying videos is a lot for phones, though. A good compromise is video on the first card and stills on the rest.

A self-hosted MP4 also works:

```html
<video src="img/piece-01-loop.mp4" autoplay muted loop playsinline></video>
```

Keep the MP4 short (5 to 10 seconds) and small (under about 4 MB).

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

The page still runs fine without the canvas.

The timecode in the bottom bar is decorative and counts 0 to 20 seconds. If it drifts out of sync with the real reel and bugs you, delete the `<div class="reel-bot">` line.

---

## 5. Adding or removing a piece

- **Add a piece:** copy a whole `<a class="tile">…</a>` block, change its number, text, image and link, and add a matching line to `pieces`.
- **Remove a piece:** delete its block and its line in `pieces`.
- Update the count in `<span class="label">4 pieces · 1080p · 24 fps</span>` so it matches.

The grid is two columns on desktop and one on phones. An even number of pieces looks best on desktop.

---

## 6. Colours and fonts

All colours are defined at the top of the `<style>` block:

```css
--phos:#6CFFB0;   /* the green accent */
--hot:#FF4D6D;    /* the red REC dot and glitch */
--void:#050807;   /* background */
```

Change `--phos` to change the accent everywhere. The fonts are **Tektur** (display) and **JetBrains Mono** (everything else), both loaded from Google Fonts.

---

## 7. Publishing your changes

1. Commit and push to this repo:

   ```zsh
   git add -A && git commit -m "Add real titles and poster frames" && git push
   ```

2. Tell Uncle Matt. The live page is served from his site (`mattcarpenter-site`, folder `michael-carpenter/`), and he copies `index.html` and `img/` over to publish.

If you ever move the site to your own domain, this folder works as-is on GitHub Pages, Netlify or Cloudflare Pages.
