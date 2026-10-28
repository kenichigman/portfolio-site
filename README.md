# portfolio-site

Source of [kenichigman.pages.dev](https://kenichigman.pages.dev) — a
single-file portfolio site on Cloudflare Pages: no build step, no
framework, one HTML file with inline CSS/JS, a hand-rolled datamosh
glitch system, and click-to-play film embeds that start at exact
timestamps.

## What it is

A portfolio for agent systems and data pipelines work, plus two
datamosh film pieces (made with the pipeline in the `music-video`
repo). The page is the artifact: it was built for a Cloudflare Build
Night in Austin, and the design treats restraint as a feature — the
glitch is loud exactly where it should be and quiet everywhere else.

## Architecture

Everything lives in `index.html` (~178 KB, self-contained apart from
the media files beside it):

- **Hero film array** — seven monitors loop short datamosh fragments
  on independent, asynchronous loops; clicking one opens the full
  film (YouTube nocookie embed) at the timestamp that fragment came
  from.
- **Snap-play film section** — a muted, looping live preview of the
  second film; a click swaps it inline for the full film with sound,
  from the beginning.
- **Sections** — the agent framework, the execution tier, the music
  video engine, stack, education, contact (GitHub + résumé; the
  résumé PDF is served by the live site and intentionally not
  re-published in this repo).

## The datamosh fx system

A small interaction budget, enforced in code: most text blocks get a
calm treatment — a fringe-only chromatic offset (≤1.5px, ~420ms) that
fires exactly once per element per page load and never displaces
layout again — while the hero and film figures keep the full glitch
bursts and may re-fire. Hover bursts are reserved for true
interactives; media clicks get the full treatment, text-link clicks
the fringe version. `prefers-reduced-motion` disables the system
entirely. The point is a page that feels alive on first scroll and
stays readable after it.

## Deploy

Cloudflare Pages, direct upload: the contents of this repo (minus
this README) are the deploy unit — upload the folder, Pages serves
it as-is. There is no build command and no output directory.

## Follow-up

A Workers version of the site is a planned follow-up (the live site
runs on Pages today). When it lands, it will land here as a visible
migration, not a silent swap.

## Files

```
index.html       the whole site
clip-*.mp4       hero-array film fragments (7)
poster*.jpg      film posters / stills
film-stills.jpg  section still
LICENSE          MIT (code; the films and stills are the author's own work)
```
