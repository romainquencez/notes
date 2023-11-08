# Git

## Commandes utiles

### Diff

```sh
git diff
```

### Lister les fichiers d'un commit

```sh
git show --name-only
```

Exemple :

```sh
commit 44e20c2a834415f760c46ad9a2ece15232fb6116 (HEAD -> appbg, tag: v0.0.40, origin/master, origin/HEAD, master)
Author: Romain Quencez <34655643+romainquencez@users.noreply.github.com>
Date:   Mon Nov 6 08:57:04 2023 +0100

    Front - Ajoute la balise meta theme-color

services/frontend/index.html
```

### Log détaillé

```sh
git log --all --graph --oneline --decorate
```

Exemple :

```sh
* 73acb23 (HEAD -> fix-exploitations, origin/fix-exploitations) Exploitations - Fix l'affichage en mobile
* 76a1e2b (origin/master, origin/HEAD, master) GitHub - Ajoute le déploiement au push de tag
| * 001a478 (origin/deploy, deploy) GitHub - Ajoute le déploiement au push de tag
|/
* c09a97c Front - Corrige le nom de l'env
* 02d0e97 Front - Ajoute l'intégration Sentry
```

## Liens utiles

- [Documentation de Git](https://git-scm.com/docs)
