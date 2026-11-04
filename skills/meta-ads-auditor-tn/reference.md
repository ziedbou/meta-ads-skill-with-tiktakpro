# Référence data TikTak — saisonnalité TN

Source : agrégat commandes non annulées / non abandonnées, companies `country` TN (ou vide),
timezone `Africa/Tunis`. Extractions prod ~nov 2026 (fenêtres 18–24 mois).

Ces chiffres **calibrent** l’interprétation Meta Ads ; ils ne remplacent pas le compte du marchand.

## Cycle salaires (jour du mois)

Sur ~3,08 M commandes / 18 mois :

| Bucket | Part | Lecture |
|--------|------|---------|
| 01–10 | 33,5 % | Post-salaire / début de mois |
| 11–20 | 32,1 % | Légèrement plus creux |
| 21–fin | 34,4 % | Anticipation fin de mois |

Jours **les plus bas** en part relative : **17, 18, 19, 20** (~3,1 %/jour vs ~3,3–3,5 % en début de mois).

Doctrine marchand (à appliquer même si l’écart agrégé est modéré) :
- **Fort** : du **20 au 10** du mois suivant
- **Faible** : du **11 au 19** (salaires déjà dépensés)

→ En fenêtre faible, une baisse CTR/CPA Meta est d’abord **calendaire**, pas créative.

## Jours de la semaine

| Jour | Part |
|------|------|
| Lun–Jeu | ~14,5–15,5 % chacun (plus forts) |
| Ven | ~14,2 % |
| Sam | ~12,7 % (plus faible) |
| Dim | ~13,3 % |

Normaliser les audits week-end vs lun–jeu.

## Mois (24 mois, volumes bruts)

Plus hauts : **juillet, octobre, mai–juin, août–sept**.  
Plus bas relatifs : **février, novembre** (hors events).

Attention : la croissance du réseau TikTak biaise les YoY — comparer **cmd/jour** dans des fenêtres de durée égale, pas les totaux bruts d’une année à l’autre.

## Events (cmd/jour, ordres de grandeur)

Exemples observés (platform-wide) :

- **Black Friday 2025** (20 nov–2 déc) : ~6380 cmd/j — pic clair
- **Fin d’année 2025** / **janvier 2026** : élevés
- **Rentrée 2025** (25 août–15 sept) : élevé mais < pic BF
- **Ramadan** : effet **variable** selon l’année et la croissance plateforme ; toujours traiter comme **régime différent** (horaires, paniers), pas comme “créa cassée”

## Échelle CPA Tunisie (vs USA)

Référence marchand TikTak (USD / résultat commande). **Tout dépend de la marge produit.**

| CPA | Lecture TN |
|-----|------------|
| < 0,50 $ | Magique |
| < 1,00 $ | Excellent |
| ≈ 1,00 $ | Très bien |
| ≈ 1,50 $ | Logique |
| ≈ 2,00 $ | À optimiser (plafond typique) |
| ≥ 3,00 $ | Souvent “ok” aux USA — **trop cher en TN** sauf grosse marge |

## Hiérarchie d’interprétation Meta (rappel)

```
calendrier salaires → event/météo/besoin → tracking → auction/CPM → créa/CTR
```

Le CTR est un **symptôme**, rarement la cause première en TN COD.
Le CPA se juge d’abord vs **marge** + échelle TN, pas vs benchmarks US.

## Origine du skill

Fork conceptuel de [kelpi-ai/meta-ads-skills](https://github.com/kelpi-ai/meta-ads-skills) :
`daily-auditor` + garde-fous `fatigue-detector`, réécrit pour TikTak / Tunisie.
