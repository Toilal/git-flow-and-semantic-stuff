---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Git et Semantic Release
drawings:
  persist: false
transition: slide-left
title: Welcome to Slidev
---

# Git et Semantic Release

Worflow et outils pour des releases 100% automatiques.

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

---
---

# Git

- [Une rapide histoire de Git](https://git-scm.com/book/fr/v2/D%C3%A9marrage-rapide-Une-rapide-histoire-de-Git)

- Au revoir CVS, SVN, Mercurial, aujourd'hui Git est le choix par défaut.

- Utilisation très permissive :
  - On peut tout faire.
  - On peut aussi faire n'importe quoi.
  - Chacun l'utilise à sa manière.

- Enorme écosystème d'outils compatibles.

---
---

# Les modèles de branchage

- [Trunk based development](https://trunkbaseddevelopment.com)

- [Git Flow](https://www.atlassian.com/fr/git/tutorials/comparing-workflows/gitflow-workflow)

*Ce sont des modèles, il faut trouver le notre, adapter aux besoins ...*

---
---

# Trunk based development

- Les développeurs collaborent tous sur la branche `trunk`.

- Réaliser les développements dans des branches à durée de vie courte (quelques 
jours maximum), validées automatiquement par la CI.

- Automatiser les tests au maximum pour valider automatiquement les changements.

- Intégrer et déployer en continu.

- Utiliser des feature flags pour désactiver les fonctionnalités non terminées/en test.

https://www.atlassian.com/fr/continuous-delivery/continuous-integration/trunk-based-development

---
---

# Feature flags

Activer / Désactiver des fonctionnalités à chaud

https://www.atlassian.com/fr/continuous-delivery/principles/feature-flags

https://flagsmith.com/

---
---

# Git Flow = 5 types de branches

- `develop`
- `main`
- `feature/*`
- `hotfix/*`
- `release/*`

---
---

# develop

Les développements terminés

Elle représente l'état actuel de tous les développements terminés, et doit toujours être prête pour la production.

# main

La production

Cette branche pointe en permance sur le dernier tag de release. Si on est sur un process de déploiement continu, elle 
représente le code actuellement déployé en production.

---
---

# feature/*

Développements en cours

Pour une nouvelle fonctionnalité, on crée une nouvelle branche nommée `feature/<nom-de-la-feature>` à partir de 
`develop`.

Chaque fonctionnalité est développé dans sa propre branche.

Lorsque la fonctionnalité est terminée, la branche est mergée dans `develop`.

*Si un bug n'est pas urgent, on peut le considérer comme une feature.*

# hotfix/*

Correctifs urgents

Pour un correctif à déployer en urgence, on crée une nouvelle branche nommée `hotfix/<nom-du-bug>` à partir de `main`.

Lorsque le correctif est terminé, la branche est mergée à la fois dans `develop` ET dans `main` (pour réaliser un 
déploiement immédiat).

*On ne passe pas par une branche de release pour intégrer un hotfix.*

---
---

# release/*

Pour intégrer les développements dans `main`

Pour réaliser une livraison intégrant les nouvelles fonctionnalités présentes dans `develop`, on crée une nouvelle 
branche nommée `release/vX.X.X` à partir de `develop`.

On peut réaliser dans cette branche tout ce qui est nécessaire pour la publication de la release (changelog, etc ...).

Lorsque la livraison est terminée, la branche est mergée dans `develop` ET dans `main` (pour réaliser un déploiement).

---
---

# GitFlow Animated

Outil de démonstration visuel

https://veerasundar.com/gitflowanimated/

Sources: https://github.com/vraa/gitflowanimated

---
---

# git-flow (command)

C'est aussi un outil en ligne de commande, et des plugins pour IDE.

- Simplifier l'usage

- Garantir le respect des conventions

- Eviter les erreurs

https://danielkummer.github.io/git-flow-cheatsheet/

---
---

# Semantic Release

Automates the whole package release workflow

- Détermine le prochain numéro de version
- Génère la release note (Changelog)
- Publie le package

https://github.com/semantic-release/semantic-release => NodeJS
https://github.com/python-semantic-release/python-semantic-release => Python

---
---

# Semantic versioning

vX.X.X

Given a version number MAJOR.MINOR.PATCH, increment the:

- MAJOR version when you make incompatible API changes
- MINOR version when you add functionality in a backward compatible manner
- PATCH version when you make backward compatible bug fixes

https://semver.org/

---
---

# Conventional commits

Signification lisible pour l'humain et pour la machine dans les messages des commits

https://www.conventionalcommits.org/fr/v1.0.0/

https://github.com/angular/angular/blob/68a6a07/CONTRIBUTING.md#commit

---
---

# Génération automatique du numéro de version

A partir de conventional commit

feat(scope): ... => MINOR VERSION

fix(scope): ... => PATCH VERSION

chore(scope): ... => No release ...

BREAKING CHANGE: => MAJOR VERSION

---
---

# Génération automatique du changelog

A partir de conventional commit

https://github.com/angular/angular/blob/main/CHANGELOG.md
https://github.com/guessit-io/guessit/blob/develop/CHANGELOG.md

---
---

# Publier l'artefact

Dans une registry

Un artefact de déploiement est le code de l'application prêt à s'executer sur la production : compilé, construit, 
minifié, optimisé ...
