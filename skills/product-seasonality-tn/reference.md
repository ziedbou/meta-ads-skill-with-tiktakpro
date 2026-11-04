# Référence — saisonnalité produits TN (TikTak)

Agrégat order_details + commandes non annulées, companies TN, ~24 mois (prod, nov 2026).
Heuristique par mots-clés dans `product_name` — indicative, pas un modèle ML.

## Pics observés

| Bucket | n lignes | Mois pic | Concentration |
|--------|----------|----------|---------------|
| Été / chaleur (clim, ventil, plage…) | ~58k | **juillet** | juin+juil ≈ **64 %** |
| Hiver / froid (chauffage, manteau…) | ~210k | **octobre** | oct–déc + jan forts |
| Rentrée (cartable, fournitures…) | ~7k | **août** | août+sept ≈ **65 %** |
| Cuisine “fêtes” (friteuse, couscoussier…) | ~2k | **mars** | fév–mars élevés (Ramadan variable) |
| Beauté (sérum, crème…) | ~63k | juillet | Relativement lissé (evergreen) |
| Tech accessoires (chargeur, coque, film…) | ~26k | juillet | Relativement lissé |
| Bracelet / montre | ~40k | juillet | Semi-plat avec bosses |

## Usage

- Confirmer un classement `product-seasonality-tn` avec la part mensuelle boutique si MCP / SQL dispo.
- Croiser avec `meta-ads-auditor-tn` (salaires, CPA TN, anti-faux-positif CTR).
