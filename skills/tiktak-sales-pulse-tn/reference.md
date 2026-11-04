# Référence — Sales Pulse TikTak (TN)

## Tools MCP (mapping)

| Intention | Tool | Notes |
|-----------|------|--------|
| KPIs jour / semaine | `analytics_overview` | `period=today\|yesterday\|week\|month` |
| CA / totaux | `analytics_sales` `metric=totals` | Corps `date_start` / `date_end` |
| Série | `analytics_sales` `metric=daily` | |
| AOV | `analytics_sales` `metric=aov` | |
| Sources | `analytics_sales` `metric=sources` | Facebook, site, … |
| Gouvernorats | `analytics_sales` `metric=gouvernorat` | Optionnel dans un pulse |
| Top produits | `analytics_top_products` | Limiter lecture top 5 |
| Ads boutique | `analytics_ads` | Croisement léger ; audit = skill Meta |
| Catalogue | `analytics_list_reports` | |

Playbook : `tiktak_playbook(topic="analytics")`.

## Fenêtres recommandées

| Demande | P | P-1 |
|---------|---|-----|
| Briefing matin | 7 j complets jusqu’à hier | 7 j avant |
| « Cette semaine » | lun→hier (semaine en cours) | même nb jours semaine préc. |
| « Le mois » | 1er → hier du mois | même période mois précédent |

Toujours **Africa/Tunis** pour « aujourd’hui / hier ».

## Calendrier liquidité (rappel)

| Jours du mois | Lecture |
|---------------|---------|
| 20 → 10 (mois suivant) | Fenêtre **forte** |
| 11 → 19 | Fenêtre **faible** — ne pas paniquer sur un creux isolé |

## Anti-patterns

- Comparer « aujourd’hui 14h » à « hier journée complète »
- Paginer `/orders` pour recalculer le CA
- Blâmer Meta sans `analytics_ads` ni skill `meta-ads-auditor-tn`
