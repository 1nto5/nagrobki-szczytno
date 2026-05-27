# nagrobkiszczytno.pl

Production site for Dariusz Twardowski - zakład kamieniarski w Szczytnie. One-page Polish-only site for a stonemason (nagrobki, parapety, blaty kuchenne).

## Tech

- **Plain HTML/CSS/JS**. No framework, no build step. Single `index.html` with inline `<style>` and `<script>`.
- Hosted free on **GitHub Pages** via Actions workflow (`.github/workflows/deploy.yml`).
- Google Fonts: Cormorant Garamond (serif headings) + Manrope (sans body).
- One JPG per service in `images/` (~0.9 MB total). Hero/nagrobek/parapet are AI-generated; blat.jpg is an Unsplash photo - replace all four with real client photos when available.

## Deployment

- Repo: `1nto5/nagrobki-szczytno` (GitHub Pages source = Actions).
- Workflow runs on push to `main`: uploads repo root as Pages artifact, deploys.
- `CNAME` contains `nagrobkiszczytno.pl` and tells Pages which custom domain to serve.
- HTTPS: Let's Encrypt cert auto-provisioned by GitHub once DNS is verified. "Enforce HTTPS" should be enabled in repo Settings > Pages.
- **One-time setup:** in repo Settings > Pages set **Source = "GitHub Actions"** before pushing.

## Domain

- Registrar: **home.pl**. First-year promo 0,99 zł netto; renewal ~100-130 zł/year.
- Set a reminder ~1 month before renewal to either renew manually or transfer to a cheaper registrar (OVH ~30-40 zł/year). Auto-renewal off.
- DNS hosted at home.pl. Nameservers: `dns.home.pl`, `dns2.home.pl`, `dns3.home.pl`.

## DNS records to set at home.pl

Managed via home.pl panel (Domeny > nagrobkiszczytno.pl > Zarządzaj rekordami DNS).

| Type  | Host  | Value            |
| ----- | ----- | ---------------- |
| A     | empty | 185.199.108.153  |
| A     | empty | 185.199.109.153  |
| A     | empty | 185.199.110.153  |
| A     | empty | 185.199.111.153  |
| CNAME | www   | 1nto5.github.io. |

### home.pl DNS quirks (from adrianantosiak.pl experience)

- Host field empty = apex (`@` is not accepted).
- External hostnames (CNAME targets) **require a trailing dot**; without it the panel rejects the record or DNS treats the name as relative.
- Own subdomains in the Host field (`www`) take **no trailing dot**.
- TTL: leave empty, default 3600 is fine.
- **Negative DNS cache after registering a `.pl` domain lasts up to 1 hour** (.pl SOA MINIMUM = 3600 s). Don't click "Verify" in GitHub Pages settings until 30-60 min after publishing records.

## SEO

- `LocalBusiness` JSON-LD in `index.html` (name, address, geo, phone, hours, services). This is what feeds Google's rich results and local pack.
- `robots.txt` allows all and points to `sitemap.xml`.
- `sitemap.xml` lists the single canonical URL.
- Canonical link + OG/Twitter Card meta tags set in `<head>`.
- Hyphens only (`-`); never em dash (`-`) or en dash (`-`) in UI strings, comments, or docs.
- **Local rankings are driven by Google Business Profile**, not the website. Set up a Profile next: same NAP as the JSON-LD here, photos of workshop + realizations, category "Stonemason / Granite supplier", service area Szczytno + powiat szczycieński.

## Phone numbers - confirm before launch

The two numbers in `index.html` came from the design draft:

- Warsztat: `+48 89 624 24 95`
- Komórka: `+48 602 358 471` (Dariusz Twardowski)

These were inserted as samples in the correct Polish format. **Verify with the client and update in three places** (hero `tel:` link, two `phone-card` blocks in `#kontakt`, and the footer + JSON-LD `telephone` field) before going live.

## To do before launch

- Confirm phone numbers (see above).
- Replace placeholder photos with real client photos (4 files in `images/`).
- Add `favicon.svg`, `favicon.ico`, `apple-touch-icon.png` to repo root (referenced in `<head>` but not yet created).
- Generate a proper 1200x630 og:image and update `og:image` meta.
- Submit `https://nagrobkiszczytno.pl/sitemap.xml` to Google Search Console.

## Conventions

- Polish only (single locale, no `/en/`).
- Hyphens only in UI text.
- Git interactions (commit messages, branch names, PR titles/descriptions) in English.
- All commits require user approval of the message before creation.
