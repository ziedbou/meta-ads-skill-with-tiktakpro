# meta-ads-skill-with-tiktakpro

Skills Claude / Cursor pour auditer les **Meta Ads** sur le marché **e-commerce Tunisie (COD TikTak PRO)**.

Fork conceptuel de [kelpi-ai/meta-ads-skills](https://github.com/kelpi-ai/meta-ads-skills) (`daily-auditor` / `fatigue-detector`), adapté avec :

- calendrier liquidité salaires TN (**20 → 10** fort, **11–19** faible)
- Ramadan / Aïd / rentrée / météo / besoin **avant** de blâmer le CTR ou la créa
- échelle **CPA Tunisie** (≠ benchmarks USA)
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
# tout le dossier skills
cp -a skills/meta-ads-auditor-tn skills/product-seasonality-tn /chemin/vers/ton-projet/.cursor/skills/

# ou Claude Code
cp -a skills/* ~/.claude/skills/
```

### Via skills CLI (si tu utilises `npx skills`)

```bash
npx skills add ziedbou/meta-ads-skill-with-tiktakpro --all
```

(à ajuster selon le support exact du CLI pour ce repo)

## Usage

1. Brancher un **Meta Ads MCP** en lecture (`https://mcp.facebook.com/ads` ou équivalent).
2. Optionnel : MCP TikTak (`analytics_ads`, commandes) pour croiser CPA boutique / marge.
3. Demander : *« audit Meta Ads Tunisie »* ou *« ce produit est-il saisonnier ? »*.

## Licence / contexte

Données de calendrier issues d’agrégats commandes TikTak (TN). Skills read-only : aucune modification de campagne sans validation humaine.
