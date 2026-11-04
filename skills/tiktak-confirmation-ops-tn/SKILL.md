---
name: tiktak-confirmation-ops-tn
description: >-
  Analyser l'ops confirmation COD TikTak PRO (Tunisie) : perf par confirmatrice/eur,
  doublons de confirmation, multi-confirmations, délais, équipe. Utiliser quand
  le taux de confirmation baisse, qu'il y a des doubles confirmations, un retard
  call center, ou « qui confirme mal » — via analytics_confirmations / analytics_team
  / orders_insights uniquement (jamais lister toutes les commandes).
---

# TikTak Confirmation Ops — Tunisie (COD)

Skill **lecture seule** pour le **call center / confirmation** d’une boutique TikTak.
À enchaîner après `tiktak-sales-pulse-tn` si le CA baisse vient plutôt de l’ops que des ads.

## Doctrine

1. **En COD, la confirmation est un levier aussi fort que la créa.** Un bon CPA Meta
   avec une mauvaise confirmation = argent brûlé.
2. **MCP analytics only.** `analytics_confirmations`, `analytics_team`,
   `analytics_orders_insights(insight="confirmations"|"cancellation")`.
   Pas de `orders_search` pour « toutes les commandes à confirmer ».
3. **Comparer P vs P-1** (7 j complets). Situer calendrier salaires TN (20→10 / 11–19).
4. **Doublons = dette ops** : chaque multi-confirmation gaspille du temps call center
   et brouille l’attribution « qui a confirmé ».
5. **Max 5 findings** + **1 action coaching / process** (pas « fire everyone »).
6. **No data → “no data”.** Ne pas inventer des taux.

## When to use

- « Les confirmations baissent », « trop de doubles confirmations »
- « Qui confirme le mieux / le pire ? »
- File d’attente qui grossit, délais de confirmation longs
- Après un pulse ventes qui montre du volume reçu mais peu de confirmé

## Prérequis

- MCP TikTak PRO
- Comprendre que les étapes pipeline varient par boutique (slugs custom possibles)

## Procédure (obligatoire)

```
0) Africa/Tunis : fenêtre salaires + event.
1) Définir P / P-1 (7 j complets jusqu’à hier, sauf demande contraire).
2) analytics_confirmations(report="per_user_per_day", date_start, date_end) sur P
   → volume par agent / jour.
3) analytics_confirmations(report="duplicates", …) sur P (et P-1 si dispo)
   → taille du problème multi-confirmations.
4) analytics_team(…) sur P et P-1
   → créées / confirmées / annulées / livrées + AOV livré-payé si présent.
5) analytics_orders_insights(insight="confirmations", …) sur P
   → délais / perf confirmation (si l’API renvoie des délais).
6) Optionnel : insight="cancellation" si annulations après tentative de conf.
7) Si une liste courte de cas est utile :
   analytics_confirmations(report="multiple", page=1, page_size≤20)
   — UNE page max, pour illustrations, pas un audit de 200K lignes.
8) Rédiger le rapport ops (format ci-dessous).
```

## Format de sortie

```markdown
# Ops confirmation — {boutique} — {période P}

**Calendrier TN :** … · **Volume multi-confirmations :** …

## Équipe (P vs P-1)
| Agent | Confirmées | Annulées | Livrées / AOV* | Δ |
(*si renvoyé par analytics_team)

## Findings (max 5)
1. Charge / déséquilibre agents
2. Doublons (2 / 3 / 4+)
3. Délais
4. Qualité (annulation post-conf, no-show livraison) si data
5. …

## Une action process (24–48 h)
Ex. : règle « 1 confirmation = 1 agent », coaching agent X, plage horaire call, …

Exemples (max 3 ids commande) si report=multiple — sinon “pas de liste”.

No changes were made.
```

## Guardrails

- Read-only : pas de changement d’étape, d’assignation bulk, ni SMS.
- Interdit : paginer `orders_*` ou `confirmations` report=multiple au-delà d’1 page illustrative.
- Interdit : blâmer un agent sans chiffres P vs P-1.
- Ne pas confondre « associées » / « créées » / « confirmées » / « livrées » — utiliser les libellés API.
- Si le sujet est Meta / CPA : renvoyer vers `meta-ads-auditor-tn` + `tiktak-sales-pulse-tn`.

## Good output looks like

Le responsable call center sait **qui** charger, **quoi** corriger sur les doublons, et **une** règle process — sans Excel de 50 colonnes.
