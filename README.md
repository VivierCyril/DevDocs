# Documentation des technologies essentiel pour DWWM

## Objectif

Mettre en place une documentation claire et simple pour les futurs stagaires sur les formation CDA/DWWM

## Commands

Sous Linux

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

Sous Windows

* `py -m mkdocs new [dir-name]` - Create a new project.
* `py -m mkdocs serve` - Start the live-reloading docs server.
* `py -m mkdocs build` - Build the documentation site.
* `py -m mkdocs -h` - Print help message and exit.

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