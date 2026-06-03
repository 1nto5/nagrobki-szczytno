# nagrobkiszczytno.pl

Production site for **Wyrób Nagrobków Dariusz Twardowski** - zakład kamieniarski w Szczytnie. One-page Polish-only site for a stonemason (nagrobki, parapety, blaty kuchenne).

## Official business name

`Wyrób Nagrobków Dariusz Twardowski` (proper case, never ALL CAPS). This is the registered name confirmed on Oferteo and Centrum Opinii directory listings. Use this exact form in `<title>`, meta description/og tags, JSON-LD `name`, header brand, footer, `llms.txt` heading, and 404 title. The `founder` field in JSON-LD and references to him as a person stay "Dariusz Twardowski".

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
- **Local rankings are driven by Google Business Profile**, not the website. The Profile **already exists, is verified, and has reviews** (as of 2026-06). Keep growing it: steady ethical review inflow, real photos of workshop + realizations, complete services. **Main category must be "Wytwórca pomników" (Monument maker)** - "Zakład kamieniarski" / "Stonemason" does NOT exist in the GBP category tree.
- **Canonical NAP (must be identical character-for-character everywhere - site, JSON-LD, GBP, directories):** name "Wyrób Nagrobków Dariusz Twardowski"; address "ul. Pomorska 16, 12-100 Szczytno"; phone "+48 509 535 051" (mobile "+48 509 535 052"); hours pon-pt 8:00-17:00, sob 9:00-13:00.
- `FAQPage` JSON-LD obok `LocalBusiness` - 8 pytań mirror-uje sekcję `#faq` na stronie **1:1 (zmiana treści wymaga edycji w obu miejscach)**. Odpowiedzi pisane answer-first (konkret w pierwszym zdaniu) pod ekstrakcję przez AI. Uwaga: bogate wyniki FAQ w Google SERP zostały wycofane - schema służy walidacji i cytowaniom AI, nie gwiazdkom w wynikach.
- `llms.txt` linkowany z `<head>` przez `rel="alternate"` + osobno serwowany z `/llms.txt`.
- Rozbudowany `LocalBusiness` JSON-LD: `founder` (Person + jobTitle), `slogan`, `knowsAbout` (20 fraz tematycznych).

## Brand brief

Stosować przy każdej edycji tekstu na stronie i w `llms.txt`:

- **Głęboka potrzeba persony** (5x Why): godna, trwała pamięć o bliskiej osobie - decyzja podejmowana raz w życiu.
- **Archetypy marki**: Opiekun (troska, spokój, formalny "Państwo") + Twórca (rzemiosło ręczne, konkretne czynności, materiały po nazwie).
- **USP**: "30 lat praktyki - od 1995. Ten sam warsztat, ten sam adres, ta sama jakość."
- **Założyciel**: ojciec pana Dariusza pracował przy wykuwaniu pomników; Dariusz przejął zakład sąsiada w 1995, pracuje samodzielnie bez podwykonawców.
- **Zakazy stylistyczne**: żadnej korpomowy ("firma", "klient", "oferta", "rozwiązania"), żadnych superlatywów ("najlepszy", "z pasją", "wysokiej jakości"), żadnego konglomeratu (klient go nie obrabia), żadnych em/en-dashów.

## Do potwierdzenia z Dariuszem przed kolejnym deployem

- **Potwierdzone jako poprawne (2026-06):** FAQ #1 (zostaje "wycena indywidualna"), FAQ #2 (4-8 tygodni), FAQ #5 (złocenie liter oferowane), FAQ #8 + `areaServed` (Pasym, Wielbark, Dźwierzuty, Jedwabno, Świętajno, Rozogi).
- Warsztat - czy historia (ojciec, przejęcie zakładu sąsiada, "bez podwykonawców") jest ścisła.

## Phone numbers

Client-confirmed numbers (in `index.html` hero CTA, both `phone-card` blocks, footer `tel:` link, and JSON-LD `telephone` field):

- `+48 509 535 051` - Warsztat
- `+48 509 535 052` - komórka

When updating, grep for `509 535` to catch every reference.

## Status / to do

- Site is **live and indexed**. Google Search Console: Domain property verified (DNS-TXT), sitemap submitted and read (status Success), homepage indexed. One stale `http://` 404 from launch day will self-resolve via the http->https redirect.
- **Still pending:** replace placeholder photos with real client photos (4 files in `images/`), then enrich alt text + add WebP. AI-generated hero/nagrobek/parapet + Unsplash blat remain until then.
- Full SEO roadmap (both ranking tracks + ready-to-paste GBP content) is in the approved plan. Open items needing Dariusz: GBP profile URL (-> JSON-LD `sameAs` + on-site links/CTA), NIP/REGON (-> footer + JSON-LD `vatID`/`taxID`), real photos.

## Conventions

- Polish only (single locale, no `/en/`).
- Hyphens only in UI text.
- Git interactions (commit messages, branch names, PR titles/descriptions) in English.
- All commits require user approval of the message before creation.
