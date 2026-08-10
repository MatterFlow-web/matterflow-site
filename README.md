# matterflow-usa.com

Static site for MatterFlow. No build step, no framework, no dependencies — three files and a
folder of assets. Hosted free on GitHub Pages.

```
index.html          the whole site
style.css           the design system
CNAME               tells GitHub which domain to serve
assets/             schematic, favicon, social card, logo
```

---

## Deploy

**1 · Create the repository**

On GitHub, make a new **public** repository. Public matters — GitHub Pages is only free on
public repos. Name it anything; `matterflow-site` is fine.

**2 · Upload the files**

Drag the *contents* of this folder into the repo (not the folder itself — `index.html` must sit
at the repository root). Commit.

**3 · Turn on Pages**

Settings → Pages → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.

Wait a minute or two. Your site appears at `https://YOURNAME.github.io/matterflow-site/`.
Confirm it looks right before touching DNS.

**4 · Add the custom domain — in GitHub first**

Settings → Pages → Custom domain → enter `matterflow-usa.com` → Save.

> Do this **before** changing DNS. Pointing DNS at GitHub before claiming the domain in your
> repo settings leaves a window where someone else could host a site on it.

**5 · DNS, at Squarespace**

Squarespace account → Domains → matterflow-usa.com → **DNS**.

Add four **A records** on the apex (host `@`):

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

And one **CNAME** so the www version works:

```
Host: www    →    YOURNAME.github.io
```

**6 · Enforce HTTPS**

Back in Settings → Pages, wait for the DNS check to pass, then tick **Enforce HTTPS**. GitHub
issues a free certificate automatically. This can take up to 24 hours; usually it's minutes.

---

## ⚠ Do not break your email

`matterflow-usa.com` is managed by **Google Workspace**. Its **MX records** are what deliver
your mail.

- **Add** the A and CNAME records above. Do not use any "reset to defaults", "remove all
  records", or bulk-replace option.
- **Leave every MX record exactly as it is.**
- Leave Domain Forwarding empty.

Changing A and CNAME records does not affect mail. Wiping the zone does. This is the single
most common way people take their own email offline during a migration.

---

## Editing

Everything is plain HTML and CSS — edit on GitHub directly (click a file, then the pencil) and
the site rebuilds in about a minute.

**Copy** lives in `index.html`, in readable sections marked by comments.
**Colours, type, and spacing** live at the top of `style.css` as custom properties. Change
`--mint` in one place and it changes everywhere.

Design tokens match `matterflow-theme.css` from the brand kit, so the site, the deck, and the
compliance report stay in step.

---

## Two things left undone

**The contact button is a `mailto:` link.** Static hosting has no server, so there is no form
handler. `mailto:` works everywhere and costs nothing, but it loses people who use webmail. If
you want a real form, [Formspree](https://formspree.io) has a free tier and needs only a form
`action` — say the word and I'll wire it in.

**There are no photographs.** The hero is the detection overlay rendered live in CSS rather
than an image. That is deliberate — it loads instantly and scales cleanly — but a real
photograph of the unit on a dock would carry more weight. Drop images into `assets/` and they
can go behind the hero with the `rgba(10,29,55,0.75)` scrim the guidelines require.

**No invented numbers.** Diversion rate, footprint, throughput, cost per ton — none appear,
because I would have had to make them up on a site whose argument is that MatterFlow logs and
proves things. One real figure from a deployment, in the pillars section, will do more work
than any sentence here.
