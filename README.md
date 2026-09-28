# NoAds Rules

A small filter list for the ads that still get through after EasyList, uBlock Origin's lists
and friends have done their job.

I maintain it alongside NoAds, a local ad blocker I'm building (not released yet). Whenever a
site still showed an ad, a wall or an empty ad box with the big lists on, and nobody upstream
had covered it yet, the fix ended up here. It's plain filter data, so you don't need NoAds to
use it.

## Using it

Add this URL as a custom list in uBlock Origin (*Filter lists → Import*), AdGuard, or anything
else that reads Adblock Plus syntax:

```
https://raw.githubusercontent.com/RealNoAds/noads-rules/main/noads.txt
```

**Use it on top of your usual lists, not instead of them.** It assumes EasyList, EasyPrivacy,
uBlock Origin's filters and, for German sites, AdGuard German are already running. On its own it
blocks next to nothing.

It updates daily (`Expires: 1 day`), and it's meant to *shrink*: when an upstream list starts
covering something, I delete my copy of it.

## What's in it

The file is split into sections, and every group of rules has a short comment saying which site
it's for and why it exists.

- **Ad-tech the big lists let through** — mostly cases where an upstream exception lets a real
  ad script load, or a host is only blocked as third-party and slips in first-party.
- **Anti-adblock walls** — blocked at the vendor where possible (`html-load.com` and friends),
  so one rule covers every site using that service.
- **First-party ad slots** — cosmetic rules for ads served from the site's own domain, keyed on
  the site's own "Anzeige"/"Advertisement" labels.
- **Surrogates** — two tracker scripts whose absence breaks the page get a harmless stub instead.
- **Unbreak** — a couple of narrow exceptions where blocking broke something real.
- **Empty boxes** — hides for reserved ad slots that stay visible and empty after the ad itself
  is blocked. I only add one after checking live that the box really is an ad slot.

## A few rules only work in NoAds

Most of the list is ordinary filters that work anywhere. A handful use things only NoAds ships,
and other blockers simply ignore them:

- `+js(adshield, …)` — needs NoAds' `adshield` scriptlet (Ad-Shield walls on Axel Springer,
  Tom's Hardware, Notebookcheck).
- `redirect=noads_bing_uet.js`, `redirect=noads_nielsen.js` — NoAds' own stub scripts.
- `$doc,replace=` and `+js(replace-node-text, …)` — need `replace` support (uBlock Origin has it).

## Found something?

If it's a general ad or tracker, or a site fix any blocker could use, please report it upstream
first — [EasyList](https://github.com/easylist/easylist/issues),
[uAssets](https://github.com/uBlockOrigin/uAssets/issues), or
[AdGuard Filters](https://github.com/AdguardTeam/AdguardFilters/issues) for German sites. A fix
there helps far more people than one here.

Open an [issue here](https://github.com/RealNoAds/noads-rules/issues) if upstream didn't take
it, if one of my rules is wrong or too broad, or if one is now redundant. The site, what you saw,
and a screenshot or the element's markup is all I need.

Pull requests are welcome too. The list is generated from annotated source files, so I'll carry
your change over by hand, credit you in the commit, and close the PR with a link to it.

## Licence

[GPL-3.0](LICENSE), the same as EasyList and uBlock Origin's lists, so rules can move freely in
either direction.
