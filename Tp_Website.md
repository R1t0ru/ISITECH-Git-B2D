# TP Website

## Initialisation & Plannification

Création d'un dépot Github, Fork la branch main, puis la cloner en local

```sh
git clone https://github.com/R1t0ru/TechStore.git
```

Récupérer les branches créées dans le dépot principal :

```sh
git remote add updstream "git@github.com:bseixeiro/TechStore.git"

git pull upstream main

git pull upstream develop
```

Ajout d'une branche pour les pages de Produits :

```sh
git checkout -b Features/Products
```

Première feature ajoutée (Cards Templates) :

```sh
git push origin -u Features/Products
```

Récupération des features de la branche Develop dans le dépot github :

```sh
git checkout develop

git pull upstream develop
```

Utilisation de commitizen et de la convention de commit :

```sh
git cz
```