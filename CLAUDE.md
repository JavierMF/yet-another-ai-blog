# Yet Another AI Blog — CLAUDE.md

Blog personal de Javier Muñoz Ferrara sobre inteligencia artificial. Bilingüe español/inglés.

## Stack

- **Engine**: Hugo v0.156+ extended (requiere Dart Sass)
- **Tema**: [hugo-theme-chirpy](https://github.com/geekifan/hugo-theme-chirpy) v1.0.3 via Hugo modules
- **Deploy**: GitHub Pages via GitHub Actions (`.github/workflows/pages.yml`)
- **Hosting del código**: https://github.com/javiermf/yet-another-ai-blog

## Servidor local

```bash
hugo server --buildDrafts
```

Abre http://localhost:1313/es/ (español) y http://localhost:1313/en/ (inglés).

## Estructura de contenido

```
content/
  es/                     # Contenido en español (idioma por defecto → URL: /)
    posts/
      YYYY-MM-DD-slug.md  # Posts con fecha en el nombre
    sobre.md              # Página estática "Sobre este blog"
    _index.md
  en/                     # Contenido en inglés (URL: /en/)
    posts/
      YYYY-MM-DD-slug.md
    about.md              # Página estática "About this blog"
    _index.md
```

## Frontmatter de los posts

Todo post **debe** incluir `type: post` para que aparezca en el listado del home (el tema filtra por este tipo):

```yaml
---
title: "Título del post"
date: 2026-06-24
type: post
categories: [Proyectos]
tags: [agentes, ia]
---
```

El archetype en `archetypes/default.md` ya lo incluye por defecto.

## Imágenes de posts

- Guardar en `static/img/posts/`
- Para SVGs: usar el shortcode `figure` en lugar de markdown `![]()` (el tema colapsa el `<img>` a 0×0 con SVGs):

```
{{< figure src="/img/posts/mi-imagen.svg" alt="Descripción" caption="Caption" width="70%" >}}
```

- Los SVGs deben tener fondo blanco explícito (`<rect width="100%" height="100%" fill="white"/>`) para verse bien en modo oscuro.
- Los SVGs deben ser XML válido: escapar `&` como `&amp;` en el contenido de texto.

## Configuración

| Fichero | Propósito |
|---|---|
| `hugo.toml` | Config raíz (baseURL, idioma por defecto, módulo del tema) |
| `config/_default/languages.toml` | Títulos, taglines, `contentDir` y menús por idioma |
| `config/_default/params.toml` | Avatar, autor, enlaces sociales |
| `config/_default/markup.toml` | Syntax highlighting, goldmark |
| `config/development/hugo.toml` | baseURL local (sobrescribe hugo.toml en dev) |
| `layouts/partials/metadata-hook.html` | CSS personalizado (título, figcaption, avatar centrado) |
| `i18n/es.yml` | Traducciones en español (copia de es-ES.yml del tema) |

## Menús del sidebar

Los menús se definen en `config/_default/languages.toml`:

```toml
[[es.menus.main]]
  name = "ℹ️ Sobre este blog"
  url = "/sobre/"
  weight = 1

[[en.menus.main]]
  name = "ℹ️ About this blog"
  url = "/en/about/"
  weight = 1
```

## Páginas estáticas

Usar `layout: page` en el frontmatter (no `type: post`):

```yaml
---
title: "Sobre este blog"
layout: page
---
```

## Crear un post nuevo

```bash
hugo new content es/posts/YYYY-MM-DD-slug.md
```

El archetype genera el frontmatter con `type: post`, `draft: true`, y campos vacíos de categories/tags.

## Añadir imágenes de posts con diagrama SVG

1. Guardar el SVG en `static/img/posts/`
2. Validar XML: `xmllint --noout static/img/posts/mi-diagrama.svg`
3. Añadir fondo blanco como primer hijo del `<svg>`: `<rect width="100%" height="100%" fill="white" rx="8"/>`
4. Referenciar con el shortcode `figure`

## Notas conocidas

- El tema usa `where .Site.RegularPages "Type" "post"` para listar posts en el home — sin `type: post` en el frontmatter el post no aparece.
- El idioma español usa código `es` pero el tema incluye `es-ES.yml`; por eso existe `i18n/es.yml` en el proyecto.
- `assets/jsconfig.json` está en `.gitignore` porque contiene rutas absolutas al cache local de Hugo modules.
