# HTML custom — plafond design TikTak (référence Niglora)

Le **meilleur design** observé sur la plateforme n’est pas une pile de
sections catalogue : c’est une **landing HTML libre** dans le bloc builder
`HTML` (`template_id` **30**, `slug` / `slug_nuxt` = `HTML`).

Exemple de référence : [niglora.tiktak-store.com](https://niglora.tiktak-store.com/)
— mono-produit COD Tunisie, RTL arabe, storytelling complet, CTA répétés,
palette forêt + crème + or.

**Objectif du skill :** aider le marchand (ou l’agent) à **écrire / itérer
son propre HTML** pour atteindre ce niveau — pas le dissuader au profit
d’un assemblage générique de sections.

## Comment ça marche techniquement

| Élément | Détail |
|---------|--------|
| Section | `template_id: 30`, champ unique `content` |
| Limite | `max_per_page: 2` → **1 ou 2 gros blocs HTML** par page (home / page CMS), pas 10 petits |
| Rendu store | `HTML.vue` injecte `values.content` dans un **Shadow DOM** (mode `open`) avec reset CSS |
| Isolation | Les styles Tailwind / thème du store **ne s’appliquent pas** dans le bloc → tout le CSS doit être **dans** le HTML |
| Édition builder | Éditeur HTML du dashboard (`content`) |
| MCP | `homepage_add_section(template_id=30, …)` puis `homepage_update_section_values(..., values={"content": "<html…>"})` |

Design section recommandé pour une landing full-bleed :
`container: "container-fluid"` (ou équivalent catalogue), paddings/margins `0`,
`background_color: "transparent"` — le HTML gère fonds et espacements.

## Deux voies (choisir avec le marchand)

| Voie | Quand | Niveau |
|------|--------|--------|
| **A — Sections catalogue** | Catalogue multi-catégories, besoin d’édition simple, peu de design | Bon / correct |
| **B — HTML custom (Niglora-like)** | Landing 1 produit, marque forte, story, conversion COD max | **Plafond plateforme** |

On peut mixer : header/nav/footer TikTak + **1–2 HTML** pour le corps de page.
Ne pas remplacer le header TikTak dans le HTML (doublons, panier cassé).

## Workflow MCP (voie B)

```
1) design_get_overview + palette/nav/fonts (cohérence header/footer boutique)
2) pages_ensure_preview
3) Si besoin : homepage_add_section(template_id=30, target="preview",
     design_overrides={container:"container-fluid", margin_*: "0", padding_*: "0"})
4) media_upload des visuels (héros, produit, lifestyle) → URLs cloudtiktak
5) Rédiger HTML self-contained (voir squelette) →
   homepage_update_section_values(section_index, values={content: "..."})
6) Captures desktop 1440 + mobile 390 (le texte n’est PAS dans le light DOM :
   juger en screenshot, pas en innerText)
7) Accordion / 2e bloc HTML si max 2 et contenu trop long
8) Accord → homepage_publish_from_preview
```

Sur une **fiche produit**, le même composant `HTML` peut vivre dans
`product_extra` / sections full-page — même règles Shadow DOM + `content`.

## Règles dures HTML (Shadow DOM)

1. **Self-contained** : `<style>…</style>` + markup dans la même string `content`.
2. **Préfixer les classes** (ex. `.ng-`, `.brand-`) — pas de classes génériques
   type `.container` / `.btn` sans préfixe.
3. **Ne pas compter sur Tailwind** du store ni sur les CSS variables thème
   (sauf si tu les répliques en dur dans ton `:root` local du bloc).
4. **Images** : URLs absolues `https://cloudtiktak.com/media/…` après `media_upload`.
   `loading="lazy"` sauf héros (`eager` + éventuellement `fetchpriority="high"`).
5. **Liens** : chemins **relatifs** (`/product/…`, `/page/…`), jamais
   `https://madomaine.tn/…` en dur.
6. **Scripts** : `innerHTML` n’exécute en général **pas** les `<script>`.
   Favoriser CSS (hover, `@keyframes`, `:target`, details/summary).
7. **RTL** : si boutique arabe, `dir="rtl"` sur le wrapper du bloc + flèches CTA
   orientées correctement.
8. **Mobile first** : breakpoints dans le `<style>` (`max-width: 767px`).
9. **Accessibilité** : vrais `h1`/`h2`, contraste, boutons `<a>` ou `<button>`,
   `alt` sur images produit.
10. **Poids** : un seul héros lourd ; compresser WebP ; éviter 10 vidéos autoplay.

## Squelette landing mono-produit (inspiré Niglora)

Ordre typique **dans un seul `content`** (sections HTML internes, pas sections builder) :

1. **Héros** — visuel produit dominant, headline locale, 1 CTA, 3 trust chips
   (livraison, COD, made in TN / garantie)
2. **Produit / formule** — 3 preuves (actif, texture, packaging) + CTA
3. **Ingrédients / preuves** — grille 3–4 items
4. **Problème** — douleur du quotidien (cartes)
5. **Preuve / science / heritage** — court, honnête (pas de claims médicaux faux)
6. **Mode d’emploi** — 3 étapes
7. **Réassurance** — livraison, paiement, support (vrais textes boutique)
8. **CTA final** → fiche produit ou ancre formulaire

Répéter le **même CTA** (libellé + couleur) 3–5 fois. Sur COD TN, le libellé
type « اطلب الآن / Commander — paiement à la livraison » convertit mieux
qu’un vague « En savoir plus ».

## Palette & UI (pattern Niglora — à adapter à la marque)

Exemple (ne pas copier aveuglément une autre niche) :

- Primary / textes : vert forêt `#163D32`
- Fond sombre sections : `#0F2A17`
- Surface crème : `#F3EBDD` / `#F6F4EC`
- Accent CTA secondaire : or `#CF924A`
- Boutons pill, `border-radius: 999px`, ombre douce
- Cards `border-radius: 16–24px`, peu d’ombres

Toujours **dériver** de la marque (logo, packaging, photos réelles).

## Mini-template de départ

```html
<style>
  .x, .x * { box-sizing: border-box; }
  .x { font-family: system-ui, sans-serif; color: #163D32; }
  .x-hero { display: grid; gap: 24px; padding: 48px 20px; background: #0F2A17; color: #fff; }
  @media (min-width: 900px) { .x-hero { grid-template-columns: 1fr 1fr; align-items: center; padding: 72px 48px; } }
  .x-btn { display: inline-flex; align-items: center; gap: 10px; padding: 16px 28px; border-radius: 999px;
           background: #CF924A; color: #fff; font-weight: 700; text-decoration: none; }
  .x-btn:hover { background: #B97F3C; }
  .x-section { padding: 56px 20px; }
  .x-section--cream { background: #F6F4EC; }
  .x-h { font-size: clamp(28px, 4vw, 44px); line-height: 1.2; margin: 0 0 12px; }
  .x-p { font-size: 16px; line-height: 1.6; opacity: .9; margin: 0 0 20px; }
  .x-grid { display: grid; gap: 16px; }
  @media (min-width: 768px) { .x-grid--3 { grid-template-columns: repeat(3, 1fr); } }
</style>
<div class="x" dir="rtl">
  <section class="x-hero">
    <div>
      <h1 class="x-h">Headline locale ici</h1>
      <p class="x-p">Une phrase de soutien. COD · livraison claire.</p>
      <a class="x-btn" href="/product/.../ton-produit">اكتشف المنتج</a>
    </div>
    <img src="https://cloudtiktak.com/media/..." alt="Produit" width="600" height="600" loading="eager" />
  </section>
  <!-- autres sections .x-section ... -->
</div>
```

Remplacer `x` par un préfixe marque ; brancher vraies URLs `media_upload` + vrai
`href` produit (`navigation_search_links` / fiche produit).

## Itération (comme un designer, pas un dump)

1. Poser structure + couleurs + 1 héros
2. Screenshot → corriger contraste / rythme
3. Ajouter 1 section à la fois
4. Vérifier mobile **avant** d’enrichir le desktop
5. Brancher tous les CTA vers la même URL conversion
6. Faire valider le marchand sur **preview**, puis publish

## Anti-patterns

- HTML qui dépend de classes Bootstrap/Tailwind du thème (cassé dans le shadow)
- 10 sections `HTML` (plafond **2**)
- Claims santé non sourcés / illégaux
- Images placeholder ou cards vides (tue le premium)
- Dupliquer header/panier TikTak dans le HTML
- Publier sur `home` sans preview
- Juger la qualité via `document.body.innerText` seulement (contenu dans le shadow)

## Quand rester en sections catalogue

Multi-catégories, maj fréquentes par non-dev, besoin de listes produits
dynamiques natives (`products_list`) sans HTML. On peut toujours **surélever**
une home catalogue avec **un** bloc HTML héros / story marque.
