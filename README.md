# NovaStack Agency Website

The official website of **NovaStack**, a digital product agency that builds
websites, web apps, mobile apps, AI calling agents, automations, Shopify
stores, WordPress sites, Meta ad campaigns, technical SEO and custom
full-stack products as one connected stack.

Live site: **https://www.novastackltd.com/**

## Services

| Service | Page |
| --- | --- |
| Websites & Web Apps | `/services/websites-web-apps` |
| Mobile App Development | `/services/mobile-app-development` |
| AI Calling Agents | `/services/ai-calling-agents` |
| n8n Automation | `/services/n8n-automation` |
| Shopify Stores | `/services/shopify-stores` |
| WordPress | `/services/wordpress` |
| Meta Ads | `/services/meta-ads` |
| Technical SEO | `/services/technical-seo` |
| Custom Full Stack | `/services/custom-full-stack` |

Legal pages: `/privacy`, `/terms`, `/terms-conditions`.

## What is in this repo

- `index.html`: the whole site in one self-contained file. It holds the
  homepage, all nine service pages, the legal pages, the project brief
  form and the FAQ. The logo is the layered diamond mark (orange outer
  diamond, green middle diamond, solid orange centre) and the site
  follows the visitor's system theme (light/dark auto).
- `README.md`: this file.
- `sitemap.xml`: homepage, nine service pages and three legal pages
  (13 URLs) on `https://www.novastackltd.com/`.
- `robots.txt`: allow-all, pointing at the sitemap.
- `netlify.toml`, `vercel.json`, `_redirects`: SPA fallback rewrites so
  direct visits and refreshes on `/services/...` and legal sub-paths serve
  `index.html` instead of returning 404.
- `docs/deploy-checklist.md`: the full deploy checklist, including the
  fallback setup for Netlify, Vercel, Cloudflare Pages, Apache/cPanel,
  Nginx, GitHub Pages and IIS, plus the post-deploy test.

## Features

- **Real clean paths.** Every service and legal page has its own URL
  (for example `/services/ai-calling-agents`), with matching canonical
  URLs, Open Graph and Twitter cards, and JSON-LD structured data
  (Organization, WebSite, Service, FAQPage, BreadcrumbList).
- **Project brief form.** Visitors pick services, describe their project
  and send it with the **Send Message** button. Submissions are sent via
  Formspree (see below) and the visitor sees an animated thank-you
  message. WhatsApp, email and call links sit beside the form.
- **Mobile first.** On phones the nine services show as a list only.
  Tapping one opens its overview directly below it, with a link to the
  full service page. Hero visuals, service pages and footer are compact
  on small screens.
- **SEO ready.** Unique titles, descriptions and keywords per page, with
  `sitemap.xml` and `robots.txt` at the domain root.

## Run locally

Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/
```

Note: `python3 -m http.server` (and opening the file directly) does not do
SPA fallback, so a direct visit to a sub-path such as
`http://localhost:8000/services/ai-calling-agents` will 404 locally. That is
expected. Navigate from the homepage instead, or use a host with the
fallback rewrites in this repo (see Deployment).

## Deployment

1. Upload `index.html` to the domain root, with `sitemap.xml` and
   `robots.txt` at the domain root too.
2. Enable the SPA fallback for your host so `/services/...`, `/privacy`,
   `/terms` and `/terms-conditions` also serve `index.html`:
   - **Netlify / Cloudflare Pages:** the `_redirects` file in this repo
     (`/* /index.html 200`) or the `[[redirects]]` rule in `netlify.toml`.
   - **Vercel:** `vercel.json` in this repo.
   - **Apache / cPanel, Nginx, GitHub Pages, IIS:** see
     `docs/deploy-checklist.md` for the exact config for each host.
3. After deploying, run the 6-step post-deploy test in
   `docs/deploy-checklist.md` (direct visit and refresh on a service page,
   `robots.txt` and `sitemap.xml` loading).
4. Do not submit anything to Google Search Console until the new site is
   actually live at `https://www.novastackltd.com/`.

## Contact form (Formspree)

The brief form posts to Formspree at
`https://formspree.io/f/mljgpbkg`. The endpoint is set in `index.html` as
`FORMSPREE_ENDPOINT`. Submissions go to the Formspree form owner. To use
a different form, replace that URL in `index.html`. Nothing else needs
to change.

## Contact

- Email: [contact@novastackltd.com](mailto:contact@novastackltd.com)
- WhatsApp / Call: [+92 339 3887766](tel:+923393887766)
- Website: https://www.novastackltd.com/

## Licence

© NovaStack. All rights reserved. This website, its copy and its logo
are the property of NovaStack and may not be reused without permission.
