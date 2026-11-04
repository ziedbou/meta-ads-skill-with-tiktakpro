# meta-ads-skill-with-tiktakpro

Skills Claude / Cursor pour auditer les **Meta Ads** sur le marché **e-commerce Tunisie (COD)**, calibrés avec les réalités des marchands **[TikTak PRO](https://tiktakpro.com/)**.

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

Ces skills ne remplacent pas le dashboard TikTak : ils aident un agent IA à **lire les Meta Ads comme un media buyer TN** (calendrier salaires, saison produit, CPA local), idéalement en croisant le **MCP TikTak** (`analytics_ads`, commandes).

---

## Pourquoi ce repo ?

Fork conceptuel de [kelpi-ai/meta-ads-skills](https://github.com/kelpi-ai/meta-ads-skills) (`daily-auditor` / `fatigue-detector`), adapté avec :

- calendrier liquidité salaires TN (**20 → 10** fort, **11–19** faible)
- Ramadan / Aïd / rentrée / météo / besoin **avant** de blâmer le CTR ou la créa
- échelle **CPA Tunisie** (≠ benchmarks USA ; plafond typique ~2 $)
- classement produit **saisonnier vs evergreen**

## Skills

| Skill | Rôle |
|-------|------|
| [`skills/meta-ads-auditor-tn`](skills/meta-ads-auditor-tn/) | Audit Meta Ads read-only (TN) |
| [`skills/product-seasonality-tn`](skills/product-seasonality-tn/) | Produit de saison ou pas + implication ads |

Chaque skill contient `SKILL.md` + `reference.md` (chiffres agrégés réseau TikTak).

## Install

### Cursor / Claude Code (projet)

```bash
cp -a skills/meta-ads-auditor-tn skills/product-seasonality-tn /chemin/vers/ton-projet/.cursor/skills/

# ou Claude Code
cp -a skills/* ~/.claude/skills/
```

### Via skills CLI

```bash
npx skills add ziedbou/meta-ads-skill-with-tiktakpro --all
```

## Usage

1. Brancher un **Meta Ads MCP** en lecture (`https://mcp.facebook.com/ads` ou équivalent).
2. Optionnel : **MCP TikTak PRO** (`analytics_ads`, commandes) pour croiser CPA boutique / marge.
3. Demander : *« audit Meta Ads Tunisie »* ou *« ce produit est-il saisonnier ? »*.

## Licence / contexte

Données de calendrier issues d’agrégats commandes TikTak (TN). Skills **read-only** : aucune modification de campagne sans validation humaine.

Produit : [TikTak PRO](https://tiktakpro.com/) · Repo skills : [github.com/ziedbou/meta-ads-skill-with-tiktakpro](https://github.com/ziedbou/meta-ads-skill-with-tiktakpro)
