# NovaStack deploy checklist (launch blocker: SPA fallback)

Prepared 24 Nov 2026, morning (Asia/Karachi). The new site is otherwise ready: dashes verified 0 in index.html on 24 Nov, 46 /services/ links, sitemap has homepage + 9 services + 3 legal pages, robots.txt is allow-all and points to the sitemap.

## The one blocker

The site is a single index.html with real paths like /services/ai-calling-agents. The host must serve index.html for those paths too (SPA fallback). Without it, a direct visit or a refresh on any service or legal page returns 404 after the domain switch, even though clicks from the homepage work.

Star has not yet said which host he will use, or confirmed his host already does this. That was asked on 23 Nov evening and is still open.

## What to upload, on any host

1. index.html at the domain root.
2. assets/robots.txt copied to /robots.txt at the domain root.
3. assets/sitemap.xml copied to /sitemap.xml at the domain root.
4. The rest of assets/ (favicon, icons, manifest) kept beside index.html, as in the build.
5. Do not submit anything to Google Search Console until the new site is actually live at www.novastackltd.com. The old site is still live there now.

## Pick one section below, by host

### Netlify
Create a file named `_redirects` at the root, containing exactly:
```
/* /index.html 200
```
Deploy as usual. No other change needed.

### Vercel
Create `vercel.json` at the root, containing:
```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }]
}
```
Deploy as usual.

### Cloudflare Pages
Create a file named `_redirects` at the root, containing exactly:
```
/* /index.html 200
```
Deploy as usual.

### Apache / cPanel shared hosting
Create or edit `.htaccess` at the domain root, containing:
```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ /index.html [L]
```
Notes: keep the existing rules if the host already has some, and add these lines. If the site lives in a subfolder rather than the domain root, say so before using this file, because the rule needs adjusting.

### Nginx (VPS / dedicated server)
In the server block for novastackltd.com, use:
```
location / {
  try_files $uri $uri/ /index.html;
}
```
Then reload Nginx. This needs server access, so it only applies if Star controls the server.

### GitHub Pages
GitHub Pages has no server rewrite. Copy index.html to a file named `404.html` in the same folder, so a direct visit to a sub-path loads the app through the 404 page. It works, but it is a workaround, not a clean fallback. Prefer Netlify, Vercel, Cloudflare Pages or Apache if possible.

### IIS (Windows hosting)
Create `web.config` at the root with a URL Rewrite rule sending all non-file requests to /index.html. Only use this if the host is actually Windows/IIS.

## Test after deploy (5 minutes)

1. Open https://www.novastackltd.com/ and confirm it shows the new site, not the old one.
2. Open https://www.novastackltd.com/services/ai-calling-agents directly in a fresh tab. It must load, not 404.
3. On that page, press refresh. It must stay on the same page, not 404.
4. Repeat step 2 for https://www.novastackltd.com/services/websites-web-apps and https://www.novastackltd.com/privacy
5. Open https://www.novastackltd.com/robots.txt and https://www.novastackltd.com/sitemap.xml and confirm both load.
6. Click a service link from the homepage, then use Next Service at the bottom of a service page, and confirm it opens the next service.

If step 2 or 3 fails, the fallback is not active yet. Do not announce the launch until they pass.

## Still needed from Star

1. Host name, or which section above applies (Netlify, Vercel, Cloudflare Pages, cPanel/Apache, Nginx, GitHub Pages, or other).
2. Whether he has checked the AI Calling and Websites & Web Apps service pages for any remaining dash, as asked on 23 Nov. File check on 24 Nov found 0 em dashes, 0 en dashes, 0 escaped dashes and 0 dash entities in index.html.

## Sources checked 24 Nov 2026

- ~/workspace/ts-spaces/novastack/index.html (234,992 bytes): em dash 0, en dash 0, escaped dash 0, dash entities 0, 46 /services/ links.
- ~/workspace/ts-spaces/novastack/assets/sitemap.xml: 13 URLs (homepage, 9 services, 3 legal pages), all https://www.novastackltd.com/ ...
- ~/workspace/ts-spaces/novastack/assets/robots.txt: allow-all, sitemap link present.
- Tracking summary: dashes removed and SEO/real paths delivered; waiting for Star's service-page check and hosting confirmation for SPA fallback.
