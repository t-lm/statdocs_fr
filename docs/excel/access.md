# Accéder aux séries

Vous allez maintenant télécharger les séries directement dans Excel.


## Télécharger un série

Pour charger un série, inscrivez dans n’importe quelle cellule de votre fichier Excel l'identifiant d’un série d'une collection publique.

Vous pouvez prendre par exemple le code eustat/apro_mk_colm/de/raw_milk_delivered qui correspond à la production totale de lait en Allemagne.

Sélectionnez la cellule avec la série, cliquez sur "Go". Et voilà, après quelques secondes, l'série est chargé en dessous de la cellule

![Installer complément](/img/user-fr_excel_access_0.png){: style="width:600px;margin:30px;padding:20px;border:1px solid #ddd;border-radius:5px"}


## Télécharger un série horizontalement

Une autre manière de charger la série ci-dessus est d'écrire dans la cellule 'get:eustat/apro_mk_colm/de/raw_milk_delivered' (sans mettre les guillemets '').

'get' est utilisé pour récupérer un série verticalement. 'geth' est utilisé pour récupérer un série de manière horizontale.

A un autre endroit de la feuille, inscrivez 'geth:eustat/apro_mk_colm/de/raw_milk_delivered' sans les guillemets.

Sélectionnez la cellule. Cliquez go. La série apparait maintenant horizontalement


## Charger plusieurs séries différents

Il est possible de charger en même temps plusieurs séries différents. Il suffit de les séparer par des virgules.

La formule 'get:xrate/monthly/eur/cad,xrate/monthly/eur/aud,xrate/monthly/eur/usd' permet de récupérer directement les trois séries de taux de change (CAD, AUD, USD) contre l'Euro.


## Charger des séries d'une même collection

Il est possible de charger des séries au sein d'une même collection (ou d'un même répertoire, souvenez vous, une collection est organisée comme un répertoire de fichiers).

Par exemple, pour obtenir tous les séries de taux de change contre l'euro, vous utilisez la commande suivante "get:xrate/monthly/eur/\*". "\*" signifie l'ensemble des séries dont l'identifiant commence par "xrate/monthly/eur/".

Cette requête retourne 31 résultats.

## Prochaines étapes

Nous avons évoqué les commandes simples pour obtenir des séries. Nous en fournirons plus dans le guide de référence.
