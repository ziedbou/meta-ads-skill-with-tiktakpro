# meta-ads-skill-with-tiktakpro

Skills Claude / Cursor pour les marchands **[TikTak PRO](https://tiktakpro.com/)** : audit **Meta Ads** Tunisie (COD), **analyse data boutique** (`analytics_*`), + **design de boutique** via MCP.

---

## À propos de TikTak PRO

**TikTak PRO** est la plateforme e-commerce tout-en-un conçue pour la **Tunisie** et l’Afrique / MENA : créer une boutique, vendre (souvent en **COD**), gérer les commandes, le stock, le tracking transporteurs et le CRM — sans empiler dix outils.

### Ce qu’elle fait

- **Boutique en ligne** — builder drag & drop, templates, pages produit / landing
- **Commandes & équipe** — confirmation, étapes, call center, manifests transporteurs
- **Paiements** — COD + paiements en ligne (écosystème TN / partenaires)
- **Livraison** — intégrations transporteurs locaux, suivi colis
- **Marketing** — pixels, ads tracking, analytics, upsells, panier abandonné
- **Support local** — FR & AR, équipe basée en Tunisie

**47 000+** boutiques créées · essai avec commandes gratuites · sans carte bancaire au départ.

### Liens publics

| | |
|---|---|
| Site | [tiktakpro.com](https://tiktakpro.com/) |
| Fonctionnalités | [tiktakpro.com/fonctionnalites](https://tiktakpro.com/fonctionnalites) |
| Tarifs | [tiktakpro.com/pricing](https://tiktakpro.com/pricing) |
| À propos | [tiktakpro.com/entreprise](https://tiktakpro.com/entreprise) |
| Contact | [tiktakpro.com/contact](https://tiktakpro.com/contact) · `contact@tiktakpro.com` · +216 55 609 111 |
| Créer une boutique | [tiktakpro.com](https://tiktakpro.com/) → *Créer ma boutique gratuitement* |

Ces skills ne remplacent pas le dashboard TikTak : ils aident un agent IA à **lire les Meta Ads et la data boutique comme un ops / media buyer TN** (calendrier salaires, saison produit, CPA local, confirmation COD) et à **composer un design boutique** via le **MCP TikTak**.

---

## Pourquoi ce repo ?

Fork conceptuel de [kelpi-ai/meta-ads-skills](https://github.com/kelpi-ai/meta-ads-skills) (`daily-auditor` / `fatigue-detector`), adapté avec :

- calendrier liquidité salaires TN (**20 → 10** fort, **11–19** faible)
- Ramadan / Aïd / rentrée / météo / besoin **avant** de blâmer le CTR ou la créa
- échelle **CPA Tunisie** (≠ benchmarks USA ; plafond typique ~2 $)
- classement produit **saisonnier vs evergreen**
- briefing **ventes** + **ops confirmation** via MCP `analytics_*` (jamais pagination commandes)

## Skills

| Skill | Rôle |
|-------|------|
| [`skills/meta-ads-auditor-tn`](skills/meta-ads-auditor-tn/) | Audit Meta Ads read-only (TN) |
| [`skills/product-seasonality-tn`](skills/product-seasonality-tn/) | Produit de saison ou pas + implication ads |
| [`skills/tiktak-sales-pulse-tn`](skills/tiktak-sales-pulse-tn/) | Briefing matin ventes / CA / AOV / top produits |
| [`skills/tiktak-confirmation-ops-tn`](skills/tiktak-confirmation-ops-tn/) | Ops confirmation COD (équipe, doublons, délais) |
| [`skills/tiktak-store-design`](skills/tiktak-store-design/) | Beau design boutique via MCP (palette → home) |

- Ads / data : `SKILL.md` + `reference.md`.
- Design : `SKILL.md` + `references/` (checklist MCP, recettes niche, home).

### Enchaînement data

```
tiktak-sales-pulse-tn
  ├─ problème ads / CPA     → product-seasonality-tn → meta-ads-auditor-tn
  └─ problème confirmation  → tiktak-confirmation-ops-tn
```

## Install

### Cursor / Claude Code (projet)

```bash
cp -a skills/meta-ads-auditor-tn skills/product-seasonality-tn \
      skills/tiktak-sales-pulse-tn skills/tiktak-confirmation-ops-tn \
      skills/tiktak-store-design \
  /chemin/vers/ton-projet/.cursor/skills/

# ou Claude Code
cp -a skills/* ~/.claude/skills/
```

### Via skills CLI

```bash
npx skills add ziedbou/meta-ads-skill-with-tiktakpro --all
```

## Usage

1. **MCP TikTak PRO** (boutique) : `analytics_*` pour data ; `design_*` / `homepage_*` pour le design.
2. Optionnel : **Meta Ads MCP** en lecture pour l’auditor ads.
3. Demander par ex. :
   - *« briefing ventes ce matin »*
   - *« analyse les confirmations / doublons »*
   - *« audit Meta Ads Tunisie »*
   - *« ce produit est-il saisonnier ? »*
   - *« refais le design de la boutique »*

## Licence / contexte

Données de calendrier issues d’agrégats commandes TikTak (TN). Skills ads **read-only** : aucune modification de campagne sans validation humaine. Le skill design **écrit** via MCP (`design_set_*`, homepage preview) — proposer avant d’appliquer, snapshots restaurables.

Produit : [TikTak PRO](https://tiktakpro.com/) · Repo skills : [github.com/ziedbou/meta-ads-skill-with-tiktakpro](https://github.com/ziedbou/meta-ads-skill-with-tiktakpro)
