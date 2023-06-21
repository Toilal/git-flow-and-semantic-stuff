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
title: Git et Semantic Release
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

- Git est le choix par défaut pour le contrôle de sources.

- Utilisation très permissive :
  - On peut tout faire.
  - On peut aussi faire n'importe quoi.
  - Chacun l'utilise à sa manière.

- Enorme écosystème d'outils supportant git.

---
---

# Les modèles de branchage

- [Trunk based development](https://www.atlassian.com/fr/continuous-delivery/continuous-integration/trunk-based-development)

- [Git Flow](https://www.atlassian.com/fr/git/tutorials/comparing-workflows/gitflow-workflow)

*Ce sont des modèles, il faut trouver le notre, adapter aux besoins ...*

---
---

# Trunk based development

- Les développeurs collaborent tous sur une branche principale `trunk`.

- Réaliser les développements dans des branches à durée de vie courte (quelques 
jours maximum), validées automatiquement par la CI.

- Automatiser les tests au maximum.

- Intégrer et déployer en continu.

- Mettre en place des feature flags.

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

Développements terminés

Elle représente l'état actuel de tous les développements terminés, et doit toujours être prête pour la production.

# main

Version distribuée

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

---
---

# hotfix/*

Correctifs urgents

Pour un correctif à déployer en urgence, on crée une nouvelle branche nommée `hotfix/<nom-du-bug>` à partir de `main`.

Lorsque le correctif est terminé, la branche est mergée à la fois dans `develop` ET dans `main` (pour réaliser un 
déploiement immédiat).

*On ne passe pas par une branche de release pour intégrer un hotfix.*

---
---

# release/*

Préparation des releases

Pour réaliser une livraison intégrant les nouvelles fonctionnalités présentes dans `develop`, on crée une nouvelle 
branche nommée `release/vX.X.X` à partir de `develop`.

On peut réaliser tout ce qui est nécessaire pour la publication de la release (changelog, versioning ...).

Lorsque la livraison est terminée, la branche est mergée dans `develop` ET dans `main`.

---
---

# support/*

Support des anciennes versions majeures

Ces branches permettent de continuer à travailler d'anciennes versions de l'application, qui nécessitent encore du 
support (correctif et backport de nouvelles fonctionnalités).

Ces branches divergent et ne seront jamais mergée dans `main` ni `develop`. Elles peuvent être alimentées par 
Cherry Pick.

---
---

# GitFlow Animated

Outil pédagogique visuel

https://veerasundar.com/gitflowanimated/

*https://github.com/vraa/gitflowanimated*

---
---

# git-flow (command)

C'est aussi un outil en ligne de commande, et des plugins pour éditeurs de code.

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
- Possibilités d'extension

https://github.com/semantic-release/semantic-release *NodeJS*

https://github.com/python-semantic-release/python-semantic-release *Python*

---
---

# Semantic versioning

vX.X.X

En partant d'un numéro de version `MAJEURE.MINEURE.PATCH`, on incrémente:

- la version MAJEURE quand on introduit un changement d'API non compatible.
- la version MINEURE quand on ajoute une fonctionnalité de manière rétro-compatible.
- la version PATCH lors qu'on corrige un bug de manière rétro-compatible.

https://semver.org/

*Cette définition implique de définir clairement les interfaces exposées publiquement.*

---
---

# Commits conventionnels

Signification lisible pour l'humain et pour la machine dans les messages des commits

https://www.conventionalcommits.org/fr/v1.0.0/

https://github.com/angular/angular/blob/68a6a07/CONTRIBUTING.md#commit

---
---

# Génération automatique du numéro de version

A partir de commits conventionnels

- feat(scope): ...
  - Version mineure

- fix(scope): ... 
  - Version patch

- chore(scope): ...
  - Pas de release

- BREAKING CHANGE: 
  - Version majeure

---
---

# Génération automatique du changelog

A partir de commits conventionnels

https://github.com/angular/angular/blob/main/CHANGELOG.md

https://github.com/guessit-io/guessit/blob/develop/CHANGELOG.md

---
---

# Publier l'artefact

Dans une registry

Un artefact de déploiement est le code de l'application prêt à s'executer sur la production : compilé, construit, 
minifié, optimisé ...

---
background: https://source.unsplash.com/collection/94734566/1920x1080
---

# Merci

Questions / Echanges
