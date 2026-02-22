# Status

## Current Phase
Validatie — Fake-door test met landing page + Meta Ads

## In Progress
- [ ] Meta Pixel ID invullen in `index.html` — Events Manager bug, Pixel aanmaken lukt niet
- [ ] Nano Banana: hogere kwaliteit versies van logo, cover, ad creative genereren

## Done (sessie 2)
- [x] Meta Ads campagne aangemaakt (€6/dag × 4 dagen = €24, wordt beoordeeld)
- [x] Facebook bedrijfspagina ingericht (logo, cover, bio)
- [x] 3 afbeeldingen gegenereerd (logo, cover, ad creative)
- [x] Ad copy geschreven + geplaatst
- [x] Targeting: Meubelmaken, Ambacht (NL, 28-55)

## Done (sessie 1)
- [x] Project structuur opgezet (.agent/, .context/)
- [x] Landing page rebranded: OptiCut AI → Zaagslim
- [x] Fake social proof verwijderd, CTA's gefixed
- [x] SEO meta description + smooth scroll
- [x] Meta Pixel base code ingebouwd (placeholder ID)
- [x] AJAX form submit + bedankpagina + Lead tracking
- [x] Nginx server block op VPS
- [x] HTML gedeployed naar `/var/www/zaagslim/`
- [x] VPS hosting geverifieerd (HTTP 200)
- [x] Logo concept gegenereerd
- [x] Ad copy variant B geschreven

## Backlog
- [ ] Hero sectie: visuele mockup/screenshot toevoegen
- [ ] Favicon toevoegen

## Known Issues
- Meta Events Manager "Gegevens koppelen" modal sluit zonder Pixel aan te maken

## Infrastructure
- **VPS**: 81.0.219.126 (Contabo)
- **SSH**: `ssh -i ~/.ssh/deploy_sniper sniper@81.0.219.126`
- **Deploy**: `scp` naar `/var/www/zaagslim/`
- **DNS**: TransIP, A-records voor @ en www

## Health Check
- Last check: 2026-02-22
- Sessions: 2
- Next due: after 5 sessions or 2 weeks
