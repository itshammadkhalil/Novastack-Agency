# NovaStack Agency Website

The official website of **NovaStack**, a digital product agency that builds
websites, web apps, mobile apps, AI calling agents, automations, Shopify
stores, WordPress sites, Meta ad campaigns, technical SEO and custom
full-stack products as one connected stack.

Live site: **https://www.novastackltd.com/**

NovaStack is one team that builds the whole stack, so a client's website,
app, AI agent and automations share the same data and work as one system,
instead of being built by separate vendors that do not talk to each other.
At launch the client gets full handover of the code, accounts and
documentation, so they can run everything themselves.

## Services

NovaStack offers nine services. Each one has its own full page on the
site, with why it matters, what it does for the business, how it is
built, what the client gets, who it is best for and its own FAQs.

| Service | Page | What it covers |
| --- | --- | --- |
| Websites & Web Apps | `/services/websites-web-apps` | Company websites, landing pages, dashboards, portals and custom web applications that are fast, responsive and SEO-ready. |
| Mobile App Development | `/services/mobile-app-development` | iOS and Android apps, built with Flutter or React Native, from idea and design to App Store and Play Store launch. |
| AI Calling Agents | `/services/ai-calling-agents` | AI voice agents that make and answer calls in a natural voice, greeting customers, answering common questions, qualifying leads, booking appointments and following up, 24/7, with every call recorded and transcribed. |
| n8n Automation | `/services/n8n-automation` | Workflow automation with n8n, connecting the tools a business already uses so repetitive work runs itself, including webhooks, Google Sheets, Slack, email and CRM updates. |
| Shopify Stores | `/services/shopify-stores` | Shopify stores from setup and theme to products, checkout, payment gateways and launch, built to sell. |
| WordPress | `/services/wordpress` | WordPress sites, from business sites and blogs to WooCommerce stores, with themes, plugins and ongoing care. |
| Meta Ads | `/services/meta-ads` | Meta (Facebook and Instagram) ad campaigns, from audience and creative to tracking, testing and optimisation. |
| Technical SEO | `/services/technical-seo` | Technical SEO: site speed, Core Web Vitals, crawl and index health, structured data and fixing the technical issues that hold rankings back. |
| Custom Full Stack | `/services/custom-full-stack` | Custom full-stack products where off-the-shelf tools are not enough, with frontend, backend, database and APIs built as one system. |

Legal pages: `/privacy`, `/terms`, `/terms-conditions`.

## How the site is put together

The homepage is one page with these sections, in order:

1. **Hero.** What NovaStack does, with a Start a Project action and a
   live look at the kind of work it builds.
2. **Services explorer.** All nine services as a list. Clicking a service
   shows its overview panel, with a link to the full service page. On
   phones the list shows on its own and the panel opens directly below
   the service that was tapped.
3. **Why NovaStack.** Why one connected team and one connected stack,
   with a diagram of how the services fit together.
4. **Every project includes.** What every project gets as standard,
   including full handover at launch and support after launch.
5. **Process.** Four steps, from brief to launch, with what is delivered
   at each step.
6. **Tech stack.** The established tools used across web, mobile,
   backend, commerce, AI and automation, including React, Next.js,
   Flutter, React Native, Node.js, PostgreSQL, Supabase, Shopify,
   WordPress, n8n, Twilio and AI voice models.
7. **FAQ.** The questions clients ask most, with plain answers.
8. **Project Brief Builder.** The form where a visitor describes their
   project and sends it (see below), with contact details beside it.

Each service page follows the same shape: a text-first hero, why the
service matters, what it does for the business, how it is built step by
step, what the client gets, who it is best for, service-specific FAQs,
related services, and a Start a Project action at the top and at the
end. The end of each service page links to the next service, wrapping
from Custom Full Stack back to Websites & Web Apps.

The legal pages (Privacy Policy, Terms of Service, Terms & Conditions)
are separate pages with the agency's honest policy in plain language.
They carry the real contact details and no invented addresses or
registration numbers.

### Navigation and URLs

Every service and legal page has its own real clean path, for example
`/services/ai-calling-agents` and `/privacy`. There are no hash URLs
for pages. The homepage sections (Services, Why NovaStack, Process,
Tech Stack, FAQ, Brief Builder) are parts of the homepage, so their
links scroll to that section without putting a `#` fragment in the
address bar. The logo and Back to NovaStack links go to the clean
homepage root `/`.

The site is a single-page application in one file, so the host must
serve `index.html` for the sub-paths (SPA fallback). Without that,
a direct visit or refresh on `/services/...` or a legal page returns
404. The fallback configs in this repo cover that (see Deployment).

### Theme

The site follows the visitor's system theme automatically (light or
dark). There is no theme switcher. The logo is the layered diamond
mark (orange outer diamond outline, green middle diamond outline,
solid orange centre diamond) on a dark tile, so it stays visible in
both light and dark mode. The same mark is used in the header, footer,
favicon and app icon.

## What is in this repo

- `index.html`: the whole site in one self-contained file. It holds the
  homepage, all nine service pages, the legal pages, the project brief
  form and the FAQ. All copy, styling and behaviour live in this one
  file, with no build step and no backend of its own.
- `README.md`: this file.
- `.htaccess`: Apache SPA fallback for Hostinger and other Apache
  hosts. It serves existing files and folders as they are and rewrites
  everything else to `/index.html`, so direct visits and refreshes on
  `/services/...`, `/privacy`, `/terms` and `/terms-conditions` work.
- `sitemap.xml`: homepage, nine service pages and three legal pages
  (13 URLs) on `https://www.novastackltd.com/`.
- `robots.txt`: allow-all, pointing at the sitemap.
- `netlify.toml`, `vercel.json`, `_redirects`: SPA fallback rewrites so
  direct visits and refreshes on `/services/...` and legal sub-paths serve
  `index.html` instead of returning 404.
- `docs/deploy-checklist.md`: the full deploy checklist, including the
  fallback setup for Netlify, Vercel, Cloudflare Pages, Apache/cPanel,
  Nginx, GitHub Pages and IIS, plus the post-deploy test.

Note: the app icons (`assets/icon-192.png` and `assets/icon-512.png`)
are not in this repo because they are binary files. They live on the
live host in the `assets/` folder. The favicon itself is an inline
data URI in `index.html`, so it works without them.

## Features

- **Real clean paths.** Every service and legal page has its own URL
  (for example `/services/ai-calling-agents`), with matching canonical
  URLs, Open Graph and Twitter cards, and JSON-LD structured data
  (Organization, WebSite, Service, FAQPage, BreadcrumbList).
- **Project brief form.** Visitors pick services, describe their project
  and send it with the **Send Message** button. Submissions are sent via
  Formspree (see below) and the visitor sees an animated thank-you
  message. WhatsApp, email and call links sit beside the form, with a
  Worldwide services note and a What happens next card (send your brief,
  we reply with a plan, build starts).
- **Mobile first.** On phones the nine services show as a list only.
  Tapping one opens its overview directly below it, with a link to the
  full service page. Hero visuals, service pages and footer are compact
  on small screens, and the desktop layout is unchanged.
- **SEO ready.** Unique titles, descriptions and keywords per page, with
  `sitemap.xml` and `robots.txt` at the domain root. Homepage sections
  are not separate pages, so they have no separate URLs and no separate
  SEO entries.
- **No invented proof.** The site makes no claims about clients,
  testimonials, statistics or addresses that were not supplied. Proof
  points are capability and process statements only.

## Project brief form (Formspree)

The brief form is the main way a visitor starts a project. It works
like this:

1. The visitor picks one or more of the nine services.
2. They fill in their name, business or company name, preferred
   timeline and a description of the project.
3. They click **Send Message**. The form checks that at least one
   service, a name and project details are filled in, and highlights
   anything missing.
4. On a successful send the form is replaced by an animated thank-you
   card ("Thank you! Your brief has been sent. We will reply shortly.")
   with a Send another message option that resets the form.
5. If the send fails, the visitor sees an error instead of a thank-you.

The form posts to Formspree at
`https://formspree.io/f/mljgpbkg`. The endpoint is set in `index.html` as
`FORMSPREE_ENDPOINT`. Submissions go to the Formspree form owner. To use
a different form, replace that URL in `index.html`. Nothing else needs
to change.

The form sends with a normal fetch first. If the browser blocks that
fetch (as some embedded previews do), it falls back to posting through
a hidden form into a hidden frame, so the brief still reaches Formspree.
While the visitor is typing, nothing is sent. The brief only leaves
the browser when they click Send Message, or when they choose to send
it themselves through WhatsApp or email. The Privacy Policy
(`/privacy`, section 2) says this in full.

Beside the form, the Talk to us directly card lists the real contact
details (email, WhatsApp and call), a Worldwide services note
("Worldwide services, remote-first, delivered online anywhere") and
three trust points (one connected team, full handover at launch,
support after launch).

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

The live site is deployed from this repo to **Hostinger as a static
website** (not as a Node.js web app, because the site has no
`package.json` and no build step). The `.htaccess` file in this repo
provides the SPA fallback on Hostinger's Apache hosting. After pushing
to `main`, redeploy or sync in Hostinger so the new commit goes live.

To deploy elsewhere:

1. Upload `index.html` to the domain root, with `sitemap.xml`,
   `robots.txt` and `.htaccess` (on Apache hosts) at the domain root too.
2. Enable the SPA fallback for your host so `/services/...`, `/privacy`,
   `/terms` and `/terms-conditions` also serve `index.html`:
   - **Hostinger / Apache / cPanel:** the `.htaccess` file in this repo.
   - **Netlify / Cloudflare Pages:** the `_redirects` file in this repo
     (`/* /index.html 200`) or the `[[redirects]]` rule in `netlify.toml`.
   - **Vercel:** `vercel.json` in this repo.
   - **Nginx, GitHub Pages, IIS:** see
     `docs/deploy-checklist.md` for the exact config for each host.
3. After deploying, run the 6-step post-deploy test in
   `docs/deploy-checklist.md` (direct visit and refresh on a service page,
   `robots.txt` and `sitemap.xml` loading).
4. Do not submit anything to Google Search Console until the new site is
   actually live at `https://www.novastackltd.com/`.

## Updating the site

The site is edited in `index.html` and pushed to this repo in separate
logical commits (one change per commit, not one big commit for
everything). A typical change is:

1. Edit `index.html` (copy, a service page, the brief form or the
   styling).
2. Check the change in the browser, including on a phone width, and
   check that no `#` fragments appear in the address bar and that the
   real service and legal paths still open.
3. Push the updated `index.html` to `main` in one commit with a clear
   message, then redeploy on Hostinger.

To change the Formspree form, replace `FORMSPREE_ENDPOINT` in
`index.html`. To change the contact details, update them in the brief
form area, the contact card, the footer and the legal pages, so all
four stay in agreement.

## Contact

- Email: [contact@novastackltd.com](mailto:contact@novastackltd.com)
- WhatsApp / Call: [+92 339 3887766](tel:+923393887766)
- Website: https://www.novastackltd.com/

## Licence

© NovaStack. All rights reserved. This website, its copy and its logo
are the property of NovaStack and may not be reused without permission.
