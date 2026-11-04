# MCP checklist — design TikTak

## Ordre des tools

1. `tiktak_playbook(topic="design")` — une fois en début de session
2. `design_get_overview()` — état des 6 zones
3. `design_list_catalog(part=…)` — `palettes` | `fonts` | `navigation` | `product_cards` | `product_page` | `category`
4. Écritures (une brique à la fois, snapshot auto) :
   - `design_apply_palette(palette_name=…)` ou `palette={…}` (8 clés)
   - `design_set_fonts(font_id=…, heading_font_id=…)`
   - `design_set_navigation(template=…, colors=…, reset_colors=False)`
   - `design_set_topbar(…)` — téléphone, marquee, liens relatifs
   - `design_set_product_card_theme(theme_id=…)` → force v2
   - `design_set_product_card_options` — sans changer de thème
   - `design_set_product_page_theme(theme_id=…)`
   - `design_set_category_page(…)`
5. Homepage :
   - `pages_ensure_preview`
   - `homepage_list_section_catalog` / `homepage_build_from_guides` / `homepage_suggest_layout`
   - `homepage_add_section` / `homepage_update_section_values` / `homepage_update_section_design` / `homepage_reorder_sections` / `homepage_remove_section` avec `target="preview"`
   - `homepage_publish_from_preview` après accord
6. Annulation : `design_list_snapshots` / `design_restore_snapshot`

## Interdits

- API REST directe
- Inventer `palette_name`, `template`, `theme_id`
- Réécrire un bloc entier `css_settings` / `store_settings` à la main
- `target="home"` sans demande explicite
- Liens menus / CTA en URL absolue
- Dire que design / homepage / sections sont « indisponibles »

## Homepage — rappel

- `website_apply_design(target="preview", apply_theme=False)` si palette déjà OK
- Preférer `homepage_build_from_guides(goal, niche, store_name)` pour une home soignée
- Après `homepage_add_section`, vérifier `sections_count` et les `template_id` dans la réponse

## Product page vs design site

| Intention | Tools |
|-----------|--------|
| Thème structure fiche produit (toute la boutique) | `design_set_product_page_theme` |
| Contenu d'**un** produit (funnel, FAQ, checkout_system) | `product_extra_*` / `product_page_setup_funnel` |

Checkout rapide dialog vs page : même composant store ; styles dialog isolés par `context="dialog"` côté storefront — hors scope MCP design.

## Robustesse MCP

Si `fetch failed` / `Not connected` : sleep ~20 s, même appel, jusqu'à 3 essais.
