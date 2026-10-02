# Olhocarro.pt

Static presentation page for **Olhocarro.pt** — a service that finds cheaper
cars abroad and works out what they'd actually cost landed in Portugal, so you
can decide whether it's worth bringing one in.

It is a **search and pricing** service, not a freight or legalisation service.
The copy is deliberately careful about that line: it promises to find cars and
do the maths, and never to handle the import itself.

> **O teu próximo destino**

One HTML file, no build step, no dependencies. Open `index.html` and it works.

---

## What's here

```
index.html            the whole page (CSS and SVG logo inlined)
assets/
  logo-mark.svg       primary logo — outlined eye, steering-wheel pupil
  favicon.svg         small-size variant, solid fill so it holds at 16px
  jingle.mp3          the jingle (6s)
  jingle.m4a          same audio, AAC, for older Safari
  og.png              1200x630 social preview
```

## The brand

The palette was sampled directly from the jingle card rather than invented, so
the site and the audio belong to the same brand:

| Role | Hex |
| --- | --- |
| Cream (background) | `#F7F1E5` |
| Navy (text) | `#112940` |
| Coral (primary accent) | `#F38561` |
| Amber (secondary) | `#F5C65A` |
| Teal (tertiary) | `#2C94B1` |

Type is **Poppins** (Google Fonts) — geometric and friendly, matching the
lettering on the jingle card.

### The logo

An eye whose pupil is a **steering wheel**: *olho* + *carro*, one mark. It reads
as automotive rather than generic-tech, which matters for a car business.

Two files on purpose. `logo-mark.svg` is the outlined version for anything
40px and up. `favicon.svg` is a solid-fill variant because the outlined eye
turns to mush below about 24px — a simplified small-size cut is deliberate, not
a duplicate.

The wordmark (`olhocarro` + `.pt` in coral) is set in CSS on the page rather
than baked into the SVG. Text inside an SVG renders with whatever font the
viewer happens to have, so a wordmark drawn that way breaks on other machines;
CSS with a webfont renders correctly for every visitor.

### The jingle

Trimmed from the original 8.9s clip to the first **6 seconds**. The remainder
was a Gemini outro card over silence (−53 dB), so nothing musical was lost. A
0.5s fade-out was added and the level normalised to −16 LUFS, because the
source peaked at 0 dB and would have clipped on some speakers.

It never autoplays — browsers block that, and it is hostile anyway. There is an
explicit play button.

---

## Running it locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Opening `index.html` straight off disk also works. A server is only worth it
because some browsers restrict `file://` media.

## Deploying

GitHub Pages serves this as-is from the default branch, root folder:
**Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.

### Pointing olhocarro.pt at it

1. At your DNS provider, for the apex domain, add four `A` records:
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
2. Add a `CNAME` record for `www` → `fabioaraujopt.github.io`
3. In **Settings → Pages → Custom domain**, enter `olhocarro.pt`. GitHub writes
   a `CNAME` file into the repo for you.
4. Tick **Enforce HTTPS** once the certificate is issued (can take an hour).

No `CNAME` file is committed here on purpose: committing one before DNS
resolves makes Pages stop serving the `github.io` URL too, so the site would go
dark while you wait.

---

## Before this goes live

Three things are deliberately unfinished — they need a decision, not code:

- **`geral@olhocarro.pt` is a placeholder.** The "Fala connosco" button points
  at it. Either create that mailbox or change the address in `index.html`.
- **`canonical` and `og:url` point at the GitHub Pages URL.** Switch both to
  `https://olhocarro.pt/` once the domain resolves, or social previews and
  search results will keep citing the github.io address. They're marked with a
  comment at the top of `index.html`.
- **The jingle was generated with Google's Gemini music tool.** Worth checking
  Google's current terms on commercial use before this fronts a business that
  takes money.

Also note the page makes no claims it can't back — no customer numbers, no
testimonials, no star ratings. Once you're actually trading in Portugal you'll
likely need to add company identification (NIF, registered name) and a link to
the *Livro de Reclamações Eletrónico*. Worth asking an accountant what applies
to your setup.
