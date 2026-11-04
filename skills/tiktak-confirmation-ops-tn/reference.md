# Référence — Confirmation Ops TikTak (TN)

## Tools MCP

| Intention | Tool | Args utiles |
|-----------|------|-------------|
| Confirmations / agent / jour | `analytics_confirmations` | `report=per_user_per_day` |
| Stats doublons | `analytics_confirmations` | `report=duplicates` |
| Liste multi-conf (échantillon) | `analytics_confirmations` | `report=multiple`, `page=1`, `page_size≤20` |
| Liste par agent | `analytics_confirmations` | `report=by_user`, `user_id=…` |
| Perf équipe globale | `analytics_team` | dates P / P-1 |
| Délais / perf confirmation | `analytics_orders_insights` | `insight=confirmations` |
| Annulations | `analytics_orders_insights` | `insight=cancellation` |
| KPIs d’une étape | `analytics_step_stats` | `step_id` requis |

Playbook : `tiktak_playbook(topic="analytics")`.

## Lectures COD typiques

| Signal | Hypothèse à tester (pas conclure seul) |
|--------|----------------------------------------|
| Reçues ↑, confirmées ↓ | Ops / horaires call / qualité leads |
| Multi-confirmations ↑ | Process (pas de lock agent) ou tool |
| Un agent << moyenne en fenêtre forte | Coaching / formation |
| Confirmées OK, livrées ↓ | Transporteur / adresse / no-show — pas la créa |
| Tout ↓ en 11–19 | Calendrier salaires — ne pas tout casser |

## Limites

- Les slugs d’étapes varient par boutique.
- `sold` produit ≠ confirmations équipe.
- Pas de restauration d’historique call depuis cette skill.
