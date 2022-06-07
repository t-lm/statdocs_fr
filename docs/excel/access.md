# Accéder aux indicateurs

Vous allez maintenant télécharger les indicateurs directement dans Excel.


## Charger un indicateur

Pour charger un indicateur, inscrivez dans n’importe quelle cellule de votre fichier Excel l'identifiant d’un indicateur d'une collection publique.

Vous pouvez prendre par exemple le code eustat/apro_mk_colm/de/raw_milk_delivered qui correspond à la production totale de lait en Allemagne.

Avec la cellule active sur l'indicateur, cliquez sur "Go". Et voilà, après quelques secondes, l'indicateur est chargé en dessous de la cellule

![Installer complément](/img/user-fr_excel_access_0.png){: style="width:600px;margin:30px;padding:20px;border:1px solid #ddd;border-radius:5px"}


## Charger un indicateur horizontalement

Une autre manière de charger l'indicateur ci-dessus est d'écrire dans la cellule "get:eustat/apro_mk_colm/de/raw_milk_delivered" (sans mettre les guillemets).

Si get est utilisé pour récupérer un indicateur, geth est utilisé pour récupérer un indicateur de manière horizontale. A un autre endroit de la feuille, inscrivez "geth:eustat/apro_mk_colm/de/raw_milk_delivered" sans les guillemets. L'indicateur apparait maintenant horizontalement


## Charger plusieurs indicateurs différents

Il est possible de charger en même temps plusieurs indicateurs différents. Il suffit de les séparer par des virgules.

La formule "get:xrate/monthly/eur/cad,xrate/monthly/eur/aud,xrate/monthly/eur/cny" permet de récupérer directement les trois indicateurs de taux de change (CAD, AUD, CNY) contre l'Euro.


## Charger des indicateurs d'une même collection

Il est possible de charger des indicateurs au sein d'une même collection ou qui possèdent les mêmes parents.

Par exemple, pour obtenir tous les indicateurs de taux de change contre l'euro, vous utilisez la commande suivante "get:xrate/monthly/eur/\*". "\*" signifie l'ensemble des indicateurs dont l'identifiant commence par "xrate/monthly/eur/".

Cette requête retourne 31 résultats.

## Prochaines étapes

Nous avons évoqué les commandes simples pour obtenir des indicateurs. Dans le guide de référence, vous retrouverez comment faire des téléchargements de gros avec la commande "batch"
