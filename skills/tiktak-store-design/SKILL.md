---
name: tiktak-store-design
description: >-
  Concevoir un beau design TikTak PRO : voie catalogue (palette, nav, cartes,
  home) OU voie premium HTML custom (bloc HTML template_id 30, Shadow DOM) pour
  atteindre un résultat type Niglora. Utiliser pour refonte, thème, landing,
  « beau site », HTML libre, landing mono-produit, ou « comme Niglora ». Toujours
  MCP + design_list_catalog pour les ids ; aider à écrire le HTML du marchand,
  ne pas le rabattre vers des sections génériques si il vise le plafond design.
---

# TikTak Store Design

Skill Claude / Cursor pour le **design de boutique TikTak PRO** via MCP
(jamais l’API REST).

## Doctrine

1. **Deux voies, un plafond.**  
   - **Voie A — catalogue** : palette → nav → cartes → pages → sections home.  
   - **Voie B — HTML custom** : 1–2 blocs `HTML` (`template_id` **30**) self-contained.  
   **Le meilleur rendu plateforme observé = voie B** (réf.
   [niglora.tiktak-store.com](https://niglora.tiktak-store.com/)).  
   Si le marchand veut un résultat « wow / landing marque », **aider à écrire
   son HTML** (`references/custom-html.md`) — ne pas le ramener par défaut
   vers un assemblage de sections génériques.
2. **MCP only.** Namespace de la boutique cible. `GetDynamicTools` puis
   `CallDynamicTool`.
3. **Playbook.** `tiktak_playbook(topic="design")` en début de session.
4. **Ids catalogue** (`design_list_catalog`, `template_id`) : ne jamais inventer.
5. **Partir de l’existant.** `design_get_overview()`.
6. **Proposer avant d’écrire** (sauf ordre impératif « fais ça »).
7. **Homepage = preview** puis publish. Pas de `target="home"` sans demande.
8. **Snapshots.** `design_restore_snapshot()` pour le design système.
9. **Beau ≠ générique IA.** Voir `references/aesthetics.md`.
10. **Valider en captures** desktop + mobile. Sur HTML custom, le contenu est
    dans le **Shadow DOM** : ne pas juger via `innerText` du light DOM.

## Choisir la voie (obligatoire en début de brief)

| Signal marchand | Voie |
|-----------------|------|
| Landing 1 produit, story, brand, « plus beau site », copy HTML déjà là | **B — HTML** |
| Catalogue large, maj faciles, grilles produits dynamiques | **A — catalogue** |
| Marque + catalogue | **Mix** : design système A + 1 HTML héros/story B |

Lire `references/custom-html.md` dès que la voie B (ou mix) est choisie.

## When to use

- Refonte / thème / look & feel / home / header / cartes
- « Fais un beau site », landing, mono-produit COD
- HTML libre, éditeur HTML, « comme Niglora », custom landing
- Palette, polices, navigation TikTak

**Ne pas** confondre avec `add-builder-section` (créer un **type** de section
en code store/backend).

## Workflow voie A (catalogue)

```
1) tiktak_playbook(topic="design")
2) design_get_overview()
3) Recette niche (references/recipes.md) + design_list_catalog
4) design_apply_palette → design_set_fonts
5) design_set_navigation → design_set_topbar
6) design_set_product_card_theme (v2)
7) design_set_product_page_theme → design_set_category_page
8) pages_ensure_preview → homepage_build_from_guides OU add_section
9) Captures → accord → homepage_publish_from_preview
```

Détail home catalogue : `references/homepage.md`.

## Workflow voie B (HTML premium)

```
1) tiktak_playbook(topic="design") + design_get_overview()
2) Aligner palette / nav / fonts (header-footer TikTak restent cohérents)
3) Lire references/custom-html.md en entier
4) pages_ensure_preview
5) Assurer 1–2 sections template_id=30 (max_per_page=2),
   design container-fluid, paddings 0
6) media_upload → URLs dans le HTML
7) Écrire / itérer values.content (HTML+CSS self-contained, préfixe classes)
8) Captures (shadow DOM) desktop + mobile
9) Accordion CTA vers la fiche produit / checkout
10) Accordion → homepage_publish_from_preview
```

Champ MCP : `homepage_update_section_values(..., values={"content": "..."})`.

## Règles dures

| Piège | Règle |
|-------|--------|
| Rabattre Niglora-like vers sections catalogue | **Non** — aider le HTML |
| > 2 blocs HTML | Plafond builder `max_per_page=2` — densifier dans 1–2 `content` |
| CSS Tailwind du thème dans le HTML | Inutile (Shadow DOM) — CSS inline dans `content` |
| Liens absolus domaine | Relatifs `/product/…` |
| Juger HTML via innerText page | Screenshots |
| Écrire sur `home` direct | Preview d’abord |
| MCP flaky | Retry ~20 s |

## Output attendu

- Voie choisie (A / B / mix) + pourquoi
- Ce qui a changé (3–6 bullets)
- Lien preview / storefront
- Captures desktop + mobile
- Prochaine étape

## Références

| Fichier | Quand |
|---------|--------|
| `references/custom-html.md` | Voie B / mix — **lire en priorité** pour un design plafond |
| `references/aesthetics.md` | Direction visuelle |
| `references/homepage.md` | Home voie A (sections) |
| `references/recipes.md` | Combos niche catalogue |
| `references/mcp-checklist.md` | Ordre tools design système |
