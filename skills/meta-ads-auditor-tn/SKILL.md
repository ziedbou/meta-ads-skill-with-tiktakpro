---
name: meta-ads-auditor-tn
description: >-
  Audit Meta Ads read-only pour e-commerce Tunisie (COD TikTak) : calendrier
  salaires 20→10, Ramadan/Aïd/rentrée/météo/besoin avant de blâmer la créa ou
  le CTR. Basé sur kelpi daily-auditor + fatigue-detector, adapté TN. Utiliser
  chaque matin ou quand le CPA/CTR bouge.
---

# Meta Ads Auditor — Tunisie (TikTak)

Adapté de **kelpi-ai/meta-ads-skills** (`daily-auditor` + doctrine `fatigue-detector`),
réécrit pour le marché tunisien COD / TikTak PRO.

## Doctrine

1. **Lire tous les jours, toucher rarement.** Read-only : proposer, ne jamais publier sans validation humaine.
2. **Le CTR n’est pas le juge de paix en Tunisie.** Une baisse de CTR ou un CPA qui monte entre le 10 et le 20 du mois, un jour de pluie, une veille de match, ou pendant un creux calendaire, n’est **pas** automatiquement une créa morte.
3. **Ordre de diagnostic (obligatoire avant “fatigue créa”)** :
   0. **Saisonnalité produit** — skill `product-seasonality-tn` : le produit est-il saisonnier / evergreen / event-driven ? Hors saison → ne pas blâmer CTR/créa
   1. Calendrier salaires / liquidité ménage
   2. Events tunisiens (Ramadan, Aïd, rentrée, soldes, Black Friday local)
   3. Météo / saison / besoin produit (ex. chauffage, plage, fournitures scolaires)
   4. Tracking (Pixel / CAPI / attribution)
   5. Auction / CPM / saturation audience
   6. **Seulement ensuite** : créa / angle / fatigue
4. **KPI métier Tunisie** : commandes livrées / payées et marge TikTak > ROAS Meta et > CTR. Toujours croiser avec `analytics_ads` / commandes boutique si MCP TikTak dispo.
5. **CPA Tunisie ≠ CPA USA.** Un CPA à **3 $** peut être “bien” aux USA ; en Tunisie le plafond réaliste est plutôt **~2 $**, et **tout dépend de la marge produit** (COGS + livraison + retour). Toujours ramener le CPA à la marge unitaire avant de dire “bon” ou “mauvais”.
6. **Max 5 findings.** Pas de dump Ads Manager.

## Échelle CPA Tunisie (référence marchand)

Montants en **USD / commande** (coût Meta par résultat purchase / lead-to-order selon le compte). Toujours pondérer par **marge réelle** du produit.

| CPA (USD) | Lecture TN |
|-----------|------------|
| **< 0,50 $** | **Magique** — scaler avec prudence (volume / qualité) |
| **< 1,00 $** | **Excellent** |
| **≈ 1,00 $** | **Très bien** |
| **≈ 1,50 $** | **Logique / acceptable** (selon marge) |
| **≈ 2,00 $** | **À optimiser** — plafond typique TN ; au-delà, alerte forte sauf très grosse marge |
| **≥ 3,00 $** | Souvent OK aux **USA**, **trop cher** en TN sauf exception marge |

Règles d’usage dans l’audit :
- Classer chaque finding budget/CPA avec cette échelle **et** une phrase marge (“marge unitaire X → CPA Y = Z % de la marge”).
- Si marge inconnue : dire “no data marge” et juger seulement vs l’échelle ci-dessus, sans inventer le COGS.
- Ne pas importer des benchmarks US (CPA 3 $ “healthy”) sans les recalibrer TN.

## Calendrier liquidité (doctrine marchand TN)

Validé / rappelé comme règle d’interprétation (pas comme loi physique) :

| Fenêtre (jour du mois, TZ Africa/Tunis) | Lecture |
|----------------------------------------|---------|
| **Du 20 au 10 du mois suivant** | Fenêtre **forte** : salaires / liquidité encore là → juger les ads plus sévèrement si ça va mal |
| **Du 11 au 19 (surtout 17–20)** | Fenêtre **faible** : salaires déjà dépensés → **ne pas tuer une créa** juste parce que CTR/CPA se dégradent |
| Week-end (sam–dim) | Demande un peu plus molle en moyenne plateforme → normaliser vs lun–jeu |

Si la fenêtre courante est **faible**, un finding “créa fatiguée” exige une preuve **hors** CTR seul (ex. fréquence très haute **et** CPA boutique qui se dégrade aussi en fenêtre forte).

## Events & saison (à checker avant toute conclusion)

Toujours situer la fenêtre d’audit :

- **Ramadan / Aïd el-Fitr / Aïd el-Adha** : volumes et horaires d’achat changent ; le soir après Iftar ≠ journée classique.
- **Rentrée scolaire** (fin août – mi-sept) : pics catégorie-dépendants.
- **Soldes / Black Friday / fin d’année / janvier** : CPM et CTR partagés avec tout le marché.
- **Saison produit** : canicule, pluie, froid — le besoin bat la créa.
- **Jours fériés / matchs / coupures** : bruit court, ne pas optimiser dessus.

Voir `reference.md` pour les ordres de grandeur observés sur le réseau TikTak (18–24 mois).

## When to use

- Audit matin d’un compte Meta Ads TN (MCP Meta read-only).
- Quand quelqu’un dit “le CTR a chuté, changeons la créa”.
- Avant de scaler ou kill une ad set.

Needs : Meta Ads MCP (read). Idéalement aussi MCP TikTak (`analytics_ads`, commandes) pour le vrai coût/commande.

## Run it

```
Audit Meta Ads TUNISIE — READ-ONLY, ne change rien.

Contexte marché : e-commerce COD Tunisie. Le CTR n’est PAS l’indicateur principal.
Ordre de diagnostic : (1) calendrier salaires 20→10 vs creux 11–19 (2) events/météo/besoin
(3) tracking (4) auction/CPM (5) créa/fatigue en dernier.

0) Classer chaque produit poussé par les ads via product-seasonality-tn
   (saisonnier/evergreen/event + saison_active oui/non). Hors saison → finding calendaire produit, pas créa.

1) Situer la fenêtre :
   - Aujourd’hui est-il dans le cycle FORT (20→10) ou FAIBLE (11–19) ?
   - Y a-t-il Ramadan/Aïd/rentrée/soldes/météo/besoin produit qui explique un creux ?

2) Comparer les 7 jours complets vs les 7 jours précédents (pas de jours partiels),
   campagne / ad set / ad : spend, résultats, coût/résultat, CTR, CPM, fréquence.
   Si possible, croiser avec commandes boutique / analytics_ads (pas seulement Meta).

3) Max 5 findings, classés par argent en jeu :
   a) Budget gaspillé (spend sans résultat crédible).
   b) CPA vs échelle TN (toujours + marge produit si dispo) :
      <0.50$ magique | <1$ excellent | ≈1$ très bien | ≈1.50$ logique |
      ≈2$ à optimiser | ≥3$ trop cher en TN (alors qu’aux USA 3$ peut être OK).
      Plafond réaliste TN ≈ 2$ — au-delà, prioriser optimisation sauf grosse marge.
   c) Dégradation “calendaire” vs vraie dégradation : si on est en creux 11–19 ou event,
      le dire clairement — NE PAS recommander un refresh créa pour ça seul.
   d) Fatigue créa : UNIQUEMENT si fréquence > 4.0 ET CTR -30% vs baseline de LA MÊME ad
      ET la dégradation tient aussi hors fenêtre faible (sinon : “probablement calendrier/marché”).
   e) Tests affamés / Pixel-CAPI (fusionner si besoin pour rester ≤5 findings).

4) Une seule prochaine action testable (hypothèse + métrique primaire + règle de kill).
   Si la vraie cause est calendaire : l’action est “tenir / réduire un peu le spend en creux”,
   PAS “jeter la créa”.

Pour chaque finding : chiffres du compte. Pas de data → “no data”, jamais inventer.
Terminer par : "No changes were made."
```

## Guardrails

- Read-only. Zéro édition campagne / budget / statut.
- **Interdit** : conclure “créa morte” sur CTR seul, surtout entre le 11 et le 19.
- Fatigue = règle à **deux conditions** (freq > 4 **et** CTR −30% vs propre baseline) **plus** filtre calendrier TN.
- Ne jamais juger une ad sur le baseline d’une autre ad.
- ROAS Meta ≠ vérité : préférer coût/commande confirmée boutique quand dispo.
- CPA : utiliser l’échelle TN (<0.5 magique … 2$ à optimiser) ; ne jamais traiter 3$ comme “bon” par défaut (réflexe US). Toujours croiser marge produit.
- Max 5 findings. Français OK (marché TN) ; garder les métriques en termes Meta standards.

## Good output looks like

Cinq puces avant le café : contexte calendrier TN en tête, chiffres réels, créa blâmée seulement si le calendrier est écarté, fin “No changes were made.”
