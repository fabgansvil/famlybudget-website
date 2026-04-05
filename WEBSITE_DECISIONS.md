# FamlyBudget Website — Decisioni e Roadmap

## Stack tecnologico scelto

| Componente | Scelta | Motivazione |
|---|---|---|
| Framework | **Astro + Firebase SDK** | Pagine statiche (SEO ottimale) + area riservata con Firebase Auth già usato dall'app |
| Hosting | **Netlify (piano gratuito)** | Uso commerciale consentito, CDN globale, SSL automatico, deploy da GitHub |
| Dominio | **famlybudget.com** (Aruba) | Acquistato e configurato |
| DNS | **Netlify DNS** | Migrato da Aruba per performance CDN ottimale |
| Autenticazione area riservata | **Firebase Auth** | Stesse credenziali dell'app mobile — zero account aggiuntivi per l'utente |

---

## Stato attuale: mockup HTML/CSS

Il file `index.html` è un mockup statico completo (HTML + CSS puro, nessun framework).
Serve come riferimento visivo per la versione definitiva in Astro.

### Sezioni implementate nel mockup

| Sezione | Stato | Note |
|---|---|---|
| Navbar | ✅ | Sticky, logo, link, CTA |
| Hero | ✅ | Headline, stats, phone mockup CSS, Google Play badge |
| Features (8 card, 2 colonne) | ✅ | Icona + testo + 3 bullet per card |
| Screenshots | ✅ CSS placeholder | Phone mockup CSS — da sostituire con screenshot reali |
| Pricing (3 piani) | ✅ | Free / Premium Local / Premium Cloud |
| CTA Banner | ✅ | |
| Footer | ✅ | Link legali, colonne navigazione |

---

## Modello Pricing implementato

| Piano | Prezzo mensile | Prezzo annuale | Storage | Note |
|---|---|---|---|---|
| **Free** | €0 | €0 | Locale o Cloud a scelta | Limiti attivi (80 tx, 3 conti, 4 ricorrenti...) |
| **Premium Local** | €2/mese | €15/anno (−38%) | Solo locale sul dispositivo | Nessun dato finanziario sul cloud |
| **Premium Cloud** | €2,99/mese | €21,99/anno (−39%) | Cloud real-time | Sync multi-dispositivo, condivisione famiglia |

### Note sul modello
- Nel piano Free l'utente sceglie liberamente il storage (toggle nelle impostazioni)
- Nel Premium il storage è bloccato al piano acquistato
- Cambiare da Premium Local a Premium Cloud richiede acquisto del piano diverso
- I bottoni "Scegli Local/Cloud/Gratis" puntano a `#download` → da aggiornare con URL Play Store reale alla pubblicazione

---

## Infrastruttura configurata ✅

- [x] Account Netlify creato (team: `famlybudget`)
- [x] Progetto Netlify: `comfy-griffin-665ddf`
- [x] Dominio `famlybudget.com` collegato come Primary Domain
- [x] `www.famlybudget.com` → redirect automatico al Primary
- [x] Netlify DNS attivo (nameserver: `dns1-4.p02.nsone.net`)
- [x] Certificato SSL/HTTPS attivo (Let's Encrypt, rinnovo automatico)
- [x] Record MX email Aruba ricreati in Netlify DNS
- [x] Record SPF, DKIM, DMARC configurati
- [x] Email `@famlybudget.com` funzionanti

---

## Step da completare — indipendenti dalla pubblicazione

### Sviluppo sito
- [ ] Convertire mockup HTML in progetto **Astro** reale
- [ ] Collegare repository GitHub a Netlify (deploy automatico su push)
- [ ] Implementare versione **responsive mobile** completa
- [ ] Pagina **Privacy Policy** (obbligatoria per Google Play)
- [ ] Pagina **Termini di Servizio**
- [ ] Pagina **Cookie Policy**
- [ ] Sezione **FAQ** (domande frequenti sui piani, storage, dati)
- [ ] Pagina **Supporto** / form di contatto

### Area riservata (post-lancio)
- [ ] Login con Firebase Auth (stesse credenziali dell'app)
- [ ] Dashboard web: visualizzazione transazioni e saldi
- [ ] Gestione abbonamento (stato Premium, upgrade/downgrade via RevenueCat)
- [ ] Pagina export dati dal browser

---

## Step subordinati alla pubblicazione su Google Play Store

- [ ] Sostituire tutti i `href="#download"` con l'URL reale del Play Store
  - Hero → badge Google Play
  - CTA banner → badge Google Play
  - Pricing → bottoni "Inizia Gratis", "Scegli Local", "Scegli Cloud"
- [ ] Sostituire i phone mockup CSS con **screenshot reali** dell'app
  - 3 screenshot: Dashboard, Transazioni, Report
  - Inserire in cornici device con Mockuphone.com o simili
- [ ] Aggiungere **badge recensioni** / numero download (dopo accumulo dati)
- [ ] Aggiungere link **App Store iOS** se/quando disponibile

---

## Note tecniche per la migrazione a Astro

```
famlybudget.com/           → pagine Astro statiche (marketing)
famlybudget.com/privacy    → Privacy Policy
famlybudget.com/terms      → Termini di Servizio
famlybudget.com/dashboard  → area riservata (Firebase Auth + SDK)
famlybudget.com/account    → gestione abbonamento RevenueCat
```

- Deploy: push su branch `main` → Netlify build automatico
- Build command: `astro build`
- Publish directory: `dist`
- Node version: 18+
