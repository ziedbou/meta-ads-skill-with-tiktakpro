---
name: tiktak-store-design
description: >-
  Concevoir et appliquer un beau design de boutique TikTak PRO via le MCP
  (palette, polices, navigation, cartes produit, page produit, catégorie,
  homepage). Utiliser dès qu'on parle de refonte, thème, look & feel, home,
  header, cartes, page produit, couleurs, ou « faire un beau site » TikTak —
  même sans le mot design. Ne jamais inventer d'ids catalogue ; toujours
  design_list_catalog + validation visuelle.
---

# TikTak Store Design

Skill Claude / Cursor pour **composer le design d'une boutique TikTak PRO**
avec le MCP TikTak (jamais l'API REST directe).

Périmètre **v1** : design site (palette → nav → cartes → page produit →
catégorie → homepage). Catalogue produits, menus de contenu, SEO : hors scope
sauf demande explicite (voir `tiktak_playbook(topic="store")`).

## Doctrine

1. **MCP only.** Namespace TikTak de la boutique cible. Toujours
   `GetDynamicTools` (schéma) puis `CallDynamicTool`. Jamais REST.
2. **Playbook d'abord.** Au démarrage d'une session design :
   `tiktak_playbook(topic="design")`. Pour une refonte boutique entière :
   `topic="store"`.
3. **Ne jamais inventer un id.** Palettes, fonts, navigation, cartes, thèmes
   page produit / catégorie → `design_list_catalog(part=…)`. Si refus outil,
   lire la liste renvoyée.
4. **Partir de l'existant.** `design_get_overview()` avant toute écriture.
5. **Proposer avant d'écrire** (2–3 options + description). Exception :
   demande impérative courte (« fais ça », « applique X ») → appliquer puis
   montrer le résultat.
6. **Ordre fixe** (la palette réécrit header / boutons / footer) :
   1. Palette (+ polices)
   2. Navigation (+ top bar)
   3. Cartes produit (v2 recommandé)
   4. Page produit
   5. Page catégorie
   6. Homepage (preview → validation → publish)
7. **Homepage = preview.** `pages_ensure_preview` → écrire sur `preview` →
   lien → accord → `homepage_publish_from_preview`. Pas de
   `target="home"` sans demande explicite.
8. **Tout est annulable.** Chaque `design_set_*` snapshot. Rappeler
   `design_restore_snapshot()`. Ne pas réécrire `css_settings` à la main.
9. **Beau ≠ générique IA.** Voir `references/aesthetics.md`. Une boutique
   high-tech ≠ cosmétique ≠ mode. Direction visuelle claire, ancrée niche.
10. **Vérifier en captures** desktop + mobile après les écritures majeures.
    Rapporter avec images, pas seulement du texte.

## When to use

- « Refais le design / le thème / le look de la boutique »
- Palette, couleurs, polices, header, navigation, top bar
- Cartes produit, page produit, page catégorie
- Homepage / accueil / sections hero / grilles produits
- « Fais un beau site » / « modernise » / « high-tech » / « mode » TikTak

**Ne pas** confondre avec :
- `add-builder-section` (ajouter un **type** de section en code)
- Skills Meta Ads (`meta-ads-auditor-tn`, `product-seasonality-tn`)

## Prérequis session

1. Identifier le **namespace MCP** de la boutique (ex. `user-tiktak-bayaphone`).
   En cas de doute : demander. Ne jamais écrire sur une autre company.
2. Confirmer niche + contraintes (ex. « pas de carousel », boutons navy,
   téléphone / adresse pour top bar).
3. Lire `references/mcp-checklist.md` avant la première écriture.
4. Choisir une **recette** dans `references/recipes.md` (ou adapter).

## Workflow (obligatoire)

```
1) tiktak_playbook(topic="design")
2) design_get_overview()
3) Niche + ambiance → proposer recette OU 2–3 options / brique
4) design_list_catalog(part="palettes"|"fonts"|…) pour les choix
5) design_apply_palette → design_set_fonts
6) design_set_navigation → design_set_topbar si besoin
7) design_set_product_card_theme (v2)
8) design_set_product_page_theme
9) design_set_category_page
10) Homepage : lire references/homepage.md
    pages_ensure_preview
    → homepage_build_from_guides OU suggest + add_section(target=preview)
    → lien preview + captures
    → après accord : homepage_publish_from_preview
11) Résumer changements + rappeler design_restore_snapshot()
```

Si la palette est déjà posée et qu'on retouche seulement la home :
`website_apply_design(..., apply_theme=False)` — sinon la palette est
réappliquée.

## Règles dures (pièges fréquents)

| Piège | Règle |
|-------|--------|
| Ids inventés | Toujours `design_list_catalog` |
| Palette après couleurs nav custom | Palette **en premier** |
| Écrire sur `home` direct | Preview d'abord |
| Liens absolus `https://domaine/…` | Chemins relatifs `/product-list/…` |
| Carousel vs grille | Demander ; défaut = grille simple (`template` liste produits) si marchand veut « affichage simple » |
| Couleurs de section codées en dur | Préférer champs couleur libres du builder ; ne pas hardcoder une palette démo |
| MCP « fetch failed » | Attendre ~20 s, réessayer (pas d'échec définitif au 1er essai) |
| Mauvaise boutique MCP | Vérifier company / namespace avant toute écriture |

## Output attendu

Après chaque vague d'écritures :
- 3–6 bullets : ce qui a changé (palette, nav, cartes, home…)
- Lien storefront / preview
- Captures desktop + mobile des zones clés (héros, cartes, une fiche produit)
- Prochaine étape claire (publier home ? ajuster X ?)

## Références (lire à la demande)

| Fichier | Quand |
|---------|--------|
| `references/mcp-checklist.md` | Avant / pendant les appels MCP |
| `references/recipes.md` | Choix niche → combo catalogue |
| `references/homepage.md` | Composition home, sections, anti-patterns |
| `references/aesthetics.md` | Direction visuelle, éviter le look IA |
