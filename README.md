<p align="center"><img src="https://flarum.org/assets/img/logo.png"></p>

<p align="center">
<a href="https://packagist.org/packages/flarum/core"><img src="https://poser.pugx.org/flarum/core/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/flarum/core"><img src="https://poser.pugx.org/flarum/core/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/flarum/core"><img src="https://poser.pugx.org/flarum/core/license.svg" alt="License"></a>
</p>

## Sur ce repos
Ce repos permet d'installer Flarum sur une instance Gandi Simple Hosting configurée en **php 7.4** (testé avec 7.4.25). Elle contient en outre les fonctionnalités supplémentaire suivantes :
- if/flajax (FlaJax 0.1.4, MathJax extension for flarum)
- fof/upload (FoF Upload 1.2.3, The file upload extension for the Flarum forum with insane intelligence.)
- clarkwinkelmann/flarum-ext-group-invitation (Group Invitation 1.0.1, Invite users into groups via links)
- flarum-lang/french (le package de langue Français 3.9.0)

**Attention ! Les tests dans d'autres version de php (8.0) n'ont pas été concluant et l'instance était très instable (plantage BDD + Apache à la connexion d'un utiisateur non admin ou non validé).**

## Installation

L'objectif et de ne pas utiliser composer sur l'instance directement, mais de passer par le [mécanimse propsé par gandi](https://docs.gandi.net/fr/simple_hosting/configurations_avancees/composer.html).

### Prérequis

- créer votre instance Gandi Simple Hosting **PHP 7.4 + MySQL 5.7**, avec un nom de domaine offert si vous ne l'avez pas déjà, définir un mot de passe. Bonne pratique : renommer correctement l'instance
- créer un site sur cette instance (éventuellement sur un sous domaine). Bonne pratique : configurer le https et se mettre en mode HTTPS only

### Installation spécifique gandi

- récupérer ce repos
- le pousser sur la branche master de votre instance gandi. Pour savoir quoi mettre à la place de ... : cf. section "deployer avec git" sur la page de configuration du *site*.
  - `git remote add gandi git+ssh ...`
  - `git push gandi main:master` (a priori, gandi s'attend d'avoir une branche master, pas main, à confirmer avec eux)
- nettoyer le vhost (supprime notamment le index.html) - /!\ uniquement pour une première installation
  - `ssh ... clean ...`
- lancer le deployement
  - `ssh ... deploy ...`

### Reprendre l'installation classique

- créer un utilisateur et une base de données associé via phpmyadmin avec droit d'accès uniquement depuis localhost
- lance rla configuration en allant sur la home page, y configurer les accès base de données
- configurer les mails en mode smtp commme indiqué dans la doc [gandi](https://docs.gandi.net/fr/simple_hosting/operations_courantes/smtp.html) mais **/!\ en explicitant le serveur smtp**, ne pas mettre locahost (cf configuration Node JS par exemple).

### Pour aller plus loin

Si besoin d'ajouter d'autre fonctionnalités, le faire depuis le repos local :
- s'assurer d'avoir exactement la même version de php que sur l'instance
- récupérer le repos
- lancer `composer install`
- rajouter les `composer require`, les mettre à jour (`composer update`) à vos risques et périls ;)
- tester en local (cf *tester en local* plus bas)
- commit
- push
- deploy (/!\ sans clean)

### Reconstruire ce repos

- Installer flarum en local avec la même verson de php comme dans la doc, y rajouter les require des features supplémentaires qu'on souhaite
- Tout remonter d'un cran pour que la racine git soit au même niveau que les composer.json et .lock
- Renomer public en htdocs
- modifier site.php pour que `'public' => __DIR__.'/htdocs'`
- et tester (cf *tester en local* plus bas)

### Tester en local
Configurer apache comme dit dans la doc flarum (module apache, module php, configuration du rewrite rules sur le vhost), créer la base, lancer la configuration flarum en allant sur localhost...


### Pour info , le guide à ne pas suivre pas à pas sur la partie conmposer
Read the **[Installation guide](https://docs.flarum.org/install)** to get started. For support, refer to the [documentation](https://docs.flarum.org/), and ask questions on the [community forum](https://discuss.flarum.org/) or [Discord chat](https://flarum.org/discord/).

## About Flarum

**[Flarum](https://flarum.org/) is a delightfully simple discussion platform for your website.** It's fast and easy to use, with all the features you need to run a successful community. It is designed to be:

* **Fast and simple.** No clutter, no bloat, no complex dependencies. Flarum is built with PHP so it’s quick and easy to deploy. The interface is powered by Mithril, a performant JavaScript framework with a tiny footprint.

* **Beautiful and responsive.** This is forum software for humans. Flarum is carefully designed to be consistent and intuitive across platforms, out-of-the-box.

* **Powerful and extensible.** Customize, extend, and integrate Flarum to suit your community. Flarum’s architecture is amazingly flexible, with a powerful Extension API.

![screenshot](https://flarum.org/assets/img/home-screenshot.png)

## Contributing

Thank you for considering contributing to Flarum! Please read the **[Contributing guide](https://docs.flarum.org/contributing)** to learn how you can help.

This repository only holds the Flarum skeleton application. Most development happens in [flarum/core](https://github.com/flarum/core).

## Security Vulnerabilities

If you discover a security vulnerability within Flarum, please follow our [security policy](https://github.com/flarum/core/security/policy) so we can address it promptly.

## License

Flarum is open-source software licensed under the [MIT License](https://github.com/flarum/flarum/blob/master/LICENSE).

