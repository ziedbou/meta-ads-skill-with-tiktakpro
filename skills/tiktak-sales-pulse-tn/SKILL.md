---
name: tiktak-sales-pulse-tn
description: >-
  Briefing matin / pulse ventes boutique TikTak PRO (Tunisie COD) : CA, volumes,
  AOV, top produits, sources, croisement ads léger. Utiliser dès qu'on demande
  un résumé du jour/semaine, « comment vont les ventes », KPIs boutique, ou un
  check data avant l'audit Meta — via MCP analytics_* uniquement (jamais paginer
  les commandes).
---

# TikTak Sales Pulse — Tunisie (COD)

Skill **lecture seule** pour un **briefing data boutique** via le MCP TikTak PRO.
Complète `meta-ads-auditor-tn` (ads) et `tiktak-confirmation-ops-tn` (équipe confirmation).

## Doctrine

1. **MCP only.** Tools `analytics_*` + `tiktak_playbook(topic="analytics")` si besoin.
   Jamais REST Django. Jamais `orders_search` en boucle pour « analyser » (lookup seulement).
2. **Comparer des fenêtres complètes** : 7 jours complets vs 7 jours précédents
   (ou mois calendaire vs mois précédent). Pas de jour partiel vs jour complet.
3. **Calendrier TN d’abord** (comme l’auditor ads) :
   - Fenêtre **forte** salaires : **20 → 10** du mois suivant
   - Fenêtre **faible** : **11 → 19**
   - Events : Ramadan / Aïd / rentrée / météo / saison produit (`product-seasonality-tn`)
4. **KPI métier COD** : commandes confirmées / livrées et CA boutique >
   vanity metrics (visiteurs seuls, CTR Meta seuls).
5. **Max 5 findings** + **1 prochaine action**. Pas de dump de tableaux.
6. **No data → “no data”.** Ne jamais inventer CA / AOV / taux.

## When to use

- « Résume les ventes », « briefing matin », « comment on a performé cette semaine »
- Avant un audit Meta Ads (contexte boutique)
- Alerte vague « ça marche moins bien » sans préciser ads vs ops

## Prérequis

- MCP TikTak PRO connecté à la boutique
- Dates en `YYYY-MM-DD`, timezone **Africa/Tunis** pour le « aujourd’hui »

## Procédure (obligatoire)

```
0) Situer le jour (Africa/Tunis) : fenêtre salaires forte/faible + event éventuel.
1) tiktak_playbook(topic="analytics") si première fois dans la session (optionnel).
2) analytics_list_reports(domain="sales") si besoin de se rappeler les metrics.
3) Fenêtres :
   - P = 7 derniers jours complets (hier inclus, pas aujourd’hui partiel)
   - P-1 = 7 jours avant P
   (Ou mois calendaire si l’utilisateur demande « le mois ».)
4) Appels MCP (parallèle si possible) :
   - analytics_overview (today / week) — pulse immédiat
   - analytics_sales(metric="totals", date_start, date_end) pour P et P-1
   - analytics_sales(metric="daily", …) pour P
   - analytics_sales(metric="aov", …) pour P et P-1
   - analytics_sales(metric="sources", …) pour P
   - analytics_top_products(…) pour P (top 5)
   - Si MCP ads / question spend : analytics_ads sur P (léger) — détail = meta-ads-auditor-tn
5) Rédiger le briefing (format ci-dessous).
6) Si le problème semble « confirmation / doublons » → enchaîner
   tiktak-confirmation-ops-tn. Si « créa / CPA Meta » → meta-ads-auditor-tn
   (+ product-seasonality-tn).
```

## Format de sortie

```markdown
# Pulse boutique — {nom} — {date}

**Calendrier TN :** forte | faible (jour X) · events : …

## Chiffres clés (P vs P-1)
| KPI | P | P-1 | Δ |
| Commandes / CA confirmé | | | |
| AOV | | | |
| Note : préciser l’étape / définition renvoyée par l’API (confirmé vs livré).

## Lecture (max 5 findings)
1. …
2. …

## Top produits (P)
- …

## Sources
- …

## Une action aujourd’hui
Hypothèse + métrique + critère de succès (24–48 h).

No changes were made.
```

## Guardrails

- Read-only. Aucune écriture produit / commande / ads.
- Interdit : `orders_search` sans filtre fort, pagination pour stats, export massif.
- Interdit : conclure « ads mortes » sur CA seul sans croiser calendrier + confirmation.
- Français OK ; garder les noms de tools MCP en anglais technique.
- Si rentabilité demandée : `analytics_profitability` / `analytics_profitability_products`
  (hors pulse minimal — le dire en 1 ligne ou basculer).

## Good output looks like

Un marchand lit ça en 90 secondes avant le café : calendrier TN, 3–5 écarts chiffrés, un geste clair, pas de jargon dashboard.
