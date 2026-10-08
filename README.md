# Documentation des technologies essentiel pour DWWM

## Objectif

Mettre en place une documentation claire et simple pour les futurs stagaires sur les formation CDA/DWWM

## Thème

[mkdocs-material](https://squidfunk.github.io/mkdocs-material/)

## Configuration

### Principe de navigation

```yml
nav:
# Premier niveau les incontournables
  - Accueil: index.md

  - Les langages:
  # Second niveau les compétences
      - Front-End:
        # Troisième niveau
          - HTML:
              - Les base: Front/html/index.md
              - Les formulaires:
                  - Les inputs: Front/html/formulaire.md
          - CSS:
              - Front/css/index.md
          - JS:
              - base: Front/javascript/index.md
              - Notions Avancée:
                  - Les évolutions de la syntaxe depuis ES5: Front/javascript/avancee.md
      - Back-end:
          - PHP: Back/php/index.md
          - SQL: Back/sql/index.md

  - Utilitaire:
      - Mkdocs: Utilitaire/mkdocs/index.md
      - Git: Utilitaire/git/index.md

  - A propos:
      - License: license
      - Release Notes: release-notes.md
```