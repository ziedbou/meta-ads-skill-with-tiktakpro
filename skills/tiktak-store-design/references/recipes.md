# Recettes design par niche

Points de départ. **Toujours vérifier** les ids avec
`design_list_catalog(part=…)` — le catalogue évolue.

Proposer la recette + 1 alternative ; laisser choisir sauf « fais ça ».

## High-tech / smartphones / électroménager

| Brique | Choix typique |
|--------|----------------|
| Palette | Bleu Corporate, Bleu Nuit & Cuivre, ou custom navy + accent orange |
| Polices | Sans-serif lisible + display technique (ex. Inter + Space Grotesk si au catalogue) |
| Navigation | Template high-tech (souvent `14`) — grande recherche + catégories |
| Cartes v2 | `catalogue` / `vitrine-tech` |
| Page produit | `classique` |
| Catégorie | Filtres ON, sous-catégories `filter_collapse` |
| Top bar | Téléphone boutique + message livraison |
| Home | Héros fort → logos marques → catégories → flash / promos → grilles produits → engagements → avis → FAQ |

## Mode / prêt-à-porter

| Brique | Choix typique |
|--------|----------------|
| Palette | Minimaliste Gris, Rose Parisien |
| Navigation | Fashion (`4`) ou éditorial (`13`) |
| Cartes v2 | `mode` |
| Page produit | `mode` ou `prestige` |
| Catégorie | Sous-catégories carrousel, bannière `force` |
| Home | Héros éditorial plein écran → lookbook / catégories → sélection → social proof |

## Cosmétique / beauté

| Brique | Choix typique |
|--------|----------------|
| Palette | Rose Gold, Lavande Douce |
| Navigation | Logo centré (`10`) ou capsule (`11`) |
| Cartes v2 | `etiquette-prix` ou `arrondi` |
| Page produit | `focus` ou `atelier` |
| Home | Héros soft → bestsellers → routine / bénéfices → avis → FAQ |

## Maison / déco

| Brique | Choix typique |
|--------|----------------|
| Palette | Sauge & Ivoire, Terracotta |
| Navigation | Classique centré (`15`) ou store (`3`) |
| Cartes v2 | `vitrine` |
| Page produit | `vitrine` ou `mosaique` |

## Alimentaire / épicerie

| Brique | Choix typique |
|--------|----------------|
| Palette | Vert Nature, Café Crème |
| Navigation | Catégories pastilles (`12`) |
| Cartes v2 | `quantite` ou `achat-rapide` |
| Page produit | `achat-rapide` |

## Custom palette (8 clés)

Si preset insuffisant, passer un objet complet :

```
primary, secondary, accent, background, surface,
text_primary, text_secondary, border
```

Exemple high-tech validé en production (inspiration, pas obligation) :
- primary `#1f5eff`, secondary `#0b1f3a`, accent `#ff7a1a`
- background `#ffffff`, surface `#f4f7fb`

Après `design_apply_palette`, retoucher boutons / badge nav si le marchand
veut navy partout sauf CTA héros orange — via les tools design / css
exposés, pas un dump manuel.

## Cartes : classic vs v2

- **v2** : une carte sur tout le site — recommandé pour cohérence.
- **classic** : chaque section home garde sa carte — éviter en refonte propre.
