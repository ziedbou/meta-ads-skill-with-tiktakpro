---
name: product-seasonality-tn
description: >-
  Classer un produit e-commerce Tunisie (TikTak) en saisonnier vs evergreen,
  nommer sa saison/fenêtre, et en déduire ce que ça change pour Meta Ads / CPA /
  lecture CTR. Utiliser avant un audit ads, un lancement, ou quand les ventes
  chutent “sans raison créa”.
---

# Product Seasonality — Tunisie (TikTak)

Complément de `meta-ads-auditor-tn`. Avant de juger une pub, **chercher si le produit est de saison**.

## Doctrine

1. **Pas tous les produits se comportent pareil.** Un clim en janvier ou un chauffage en juillet qui “perd du CTR” n’est souvent pas une créa morte : le **besoin** a disparu.
2. **Toujours classer le produit d’abord** : `saisonnier` | `semi-saisonnier` | `evergreen` | `event-driven` (Ramadan, rentrée, Aïd…).
3. **Si saisonnier hors saison** : ne pas optimiser agressivement la créa ; réduire spend, pivoter l’offre, ou attendre la fenêtre.
4. **Si evergreen** : là seulement, calendrier salaires + créa/CPA redeviennent les leviers principaux (voir `meta-ads-auditor-tn`).
5. S’appuyer sur le **nom / catégorie / attributs** du produit +, si dispo, historique commandes boutique (`analytics_*` / ventes par mois).

## Procédure (obligatoire)

Pour chaque produit (ou ad → produit) analysé :

```
1) Lire nom + catégorie + variantes.
2) Matcher les lexiques TN ci-dessous → type + fenêtre.
3) Dire explicitement :
   - type: saisonnier | semi-saisonnier | evergreen | event-driven
   - saison_active: oui/non aujourd’hui (Africa/Tunis)
   - fenêtre_idéale: mois ou events
   - implication_ads: une phrase (tenir / réduire / scaler / ne pas blâmer CTR)
4) Si historique ventes dispo : confirmer le pic mois (part des ventes).
5) Si ambigu : “semi-saisonnier / à confirmer par data”, ne pas forcer.
```

## Lexiques & fenêtres TN (calibrés data TikTak)

Ordres de grandeur observés sur le réseau (24 mois, cmd non annulées) — voir `reference.md`.

### Forte saisonnalité

| Signal produit (exemples) | Type | Fenêtre forte TN | Hors saison |
|---------------------------|------|------------------|-------------|
| Clim, ventilateur, cooler, plage, maillot, tong, sandale, parasol, piscine | **Saisonnier été** | **Mai–août** (pic juin–juillet ~65 % des ventes “chaleur”) | Ne pas juger la créa en hiver |
| Chauffage, radiateur, couverture lourde, manteau, doudoune, chauffe | **Saisonnier hiver** | **Oct–jan** (oct–déc forts) | Creux été = normal |
| Cartable, trousse, fournitures scolaires, sac scolaire | **Event rentrée** | **Fin août–mi-sept** (~65 % août+sept) | Hors rentrée = volume faible attendu |
| Couscoussier / gros volume cuisine “fêtes” (selon offre) | **Event Ramadan / fêtes** | Autour **Ramadan** (souvent fév–avr selon année) | Comparer à la même période N-1 |

### Evergreen / faible saisonnalité

| Signal | Type | Note |
|--------|------|------|
| Sérum, crème, masque, parfum, maquillage | **Evergreen beauté** | Légère bosse été possible, pas une saison stricte |
| Chargeur, câble, coque, film/verre trempé, powerbank, écouteurs | **Evergreen tech accessoire** | Relativement plat sur l’année |
| Bracelet / montre connectée (hors promo event) | **Semi-evergreen** | Présent toute l’année, petites bosses |

### Règle d’or Meta Ads

- **Produit saisonnier + hors saison** → CTR/CPA dégradés ≠ kill créa. Action typique : **couper ou minimiser le spend**, préparer le stock/créas pour la prochaine fenêtre.
- **Produit saisonnier + dans la saison** → appliquer l’échelle CPA TN + calendrier salaires (`meta-ads-auditor-tn`).
- **Evergreen** → ne pas invoquer “c’est la saison” pour excuser un CPA à 2–3 $ sans preuve.

## Run it

```
Classement saisonnalité produit TUNISIE — pour chaque produit lié aux ads / au catalogue :

1) type (saisonnier été | saisonnier hiver | event-driven | semi-saisonnier | evergreen)
2) saison_active maintenant ? (oui/non) + fenêtre idéale
3) preuves : mots du nom/catégorie et/ou % ventes par mois si data
4) implication Meta Ads en 1 phrase (scaler / tenir / réduire spend / ne pas blâmer CTR)
5) si audit ads suit : rappeler de lire meta-ads-auditor-tn APRÈS ce classement

Ne change rien aux campagnes. Pas d’invention de chiffres sans data.
```

## Guardrails

- Ne pas inventer une saison si le produit est clairement evergreen.
- Ne pas absoudre un mauvais CPA evergreen avec “météo”.
- Ramadan / Aïd / rentrée = **events** (dates mobiles) : toujours situer l’année en cours.
- Français OK ; rester factuel.

## Good output looks like

Une ligne par produit : `Clim X — saisonnier été — HORS saison (nov) — ne pas killer la créa, couper spend jusqu’à mai.`
