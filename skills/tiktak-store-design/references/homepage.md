# Homepage — composition & anti-patterns

## Squelette recommandé (e-commerce TN)

Ordre typique (à adapter niche) :

1. **Héros** — 1 composition, marque forte, 1 CTA principal (slides réelles boutique, pas stock générique)
2. **Preuve / marques** — logos partenaires ou marques vendues
3. **Catégories** — cartes cliquables vers `/product-list/…` ou `/search?…`
4. **Urgence / promo** (optionnel) — flash, tuiles promo, textes & liens **réels**
5. **Produits** — 2 à 4 rangées (nouveautés, best-sellers, catégories clés)
6. **Réassurance** — livraison, COD, garantie, support (vraies infos boutique)
7. **Avis** — Google / clients réels si dispo
8. **FAQ** — objections COD / livraison / retours

Une section = **un job**, un titre, une phrase de soutien max.

## Affichage produits : grille vs carousel

| Demande marchand | Préférer |
|------------------|----------|
| « Affichage simple », catalogue, high-tech | **Grille fixe** (ex. template liste produits ~ id `10`) — 3–4 / ligne desktop, 2 mobile |
| « Glisser », look magasin mode | Carousel / slider (ex. template ~ id `25`) |

Ne pas empiler onglets + 4 carrousels + flash sans respiration.

Champs utiles grille (design section) :
- `products_by_row_desktop` : `col-md-3` ≈ 4/ligne, `col-md-4` ≈ 3/ligne
- `products_by_row_mobile` : `col-6` ≈ 2/ligne

`products_list` : `dynamic: true`, `length` 8–12, `sort_by` (`sold`, `-created_at`),
`categories_in`, `have_discount`.

## Contenu honnête

- Remplacer textes démo (« livraison dès 50 DT » si faux)
- CTA → chemins relatifs valides (`navigation_search_links` si doute)
- Avis : vrais avis Google / clients, pas Lorem
- Images héros : photos boutique / produit, pas placeholders catalogue section

## Tools home

```
pages_ensure_preview
homepage_build_from_guides(goal, niche, store_name)   # recommandé
# ou manuel :
homepage_suggest_layout → homepage_view_section_previews
homepage_add_section(template_id, index, target="preview", values_overrides, design_overrides)
homepage_update_section_values / homepage_update_section_design
homepage_reorder_sections / homepage_remove_section
# après accord :
homepage_publish_from_preview
```

Après un add : vérifier indices — une suppression décale tout
(`remove` plusieurs fois au même index si on retire une série).

## Anti-patterns

- Premier viewport saturé (stats + promos + 3 CTA + carousel)
- Cards partout (bordures / ombres inutiles) sur le héros
- Purple gradient / cream+terracotta / look « IA générique » sans lien niche
- Écrire sur `target="home"` « pour aller plus vite »
- Dupliquer grilles ET carrousels pour les mêmes catégories
- Boutons fantômes vers `/products` si la boutique utilise `/product-list/…`
