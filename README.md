##                                                                                   LA VIE EN VERT !



# Introduction
Cette page Github a été créé par moi-même (Alexandra Renard) à l'occasion de ma formation Master 2 DEFI pour l'examen final du cours de Datavisualition de Monsieur Courtin. 
Comme souvent répété en cours, le plus important ce sont le thème choisi et les jeux de données. J'ai eu du mal à trouver des jeux de données car soit ils étaient compliqués à utiliser soit ils n'étaient pas à mon goût (thématique). Après de nombreuses recherches, sur [data.gouv.fr](https://www.data.gouv.fr/fr/), [data.culture](https://data.culture.gouv.fr/pages/home/) et [Opendatasoft](https://www.opendatasoft.com/fr/), j'ai finalement trouvé, sur ce dernier, un jeu de données.

Après avoir choisi un jeu de données sur "les arbres" , je me suis dirigée vers le sujet autour de la végétation parisienne avec une petite partie comparative sur la végétation rennaise. 

![alt tag](https://user-images.githubusercontent.com/77047183/106200477-54876180-61b7-11eb-87c2-9b2808cc96c5.jpg)

_Source: Un projet de réaménagement des Champs-Elysées est à l’étude. Il prévoit de faire une large place aux jardins et à la végétation. PCA-STREAM, Le Parisien, 11 Janvier 2021_ Lien : https://www.leparisien.fr/paris-75/paris-anne-hidalgo-promet-un-jardin-extraordinaire-sur-les-champs-elysees-11-01-2021-8418444.php


# Visualisation des données : utilisation de l'outils Cartes sur Opendatasoft

**1. La vie en vert au sein du Grand Paris **

Pour commencer à aborder ce sujet, j'ai fait le choix d'avoir une vue d'ensemble de ces données en utilisant l'outil Cartes sur Opendatasoft. 
Nous allons débuter par observer la végétation dans la ville de Paris. Le jeu de données choisi se nomme "Les arbres. 
La source est [https://opendata.paris.fr/explore/dataset/les-arbres/information/?disjunctive.typeemplacement&disjunctive.arrondissement&disjunctive.libellefrancais&disjunctive.genre&disjunctive.espece&disjunctive.varieteoucultivar&disjunctive.stadedeveloppement&disjunctive.remarquable](ParisData) et le producteur est la _Direction des Espaces Verts et de l'Environnement - Ville de Paris_. Ce jeu de donnée a pour objectif de montrer l'ensemble des arbres présents à Paris et dans ses envrions proches (Grand Paris). Les données datent du 22 Janvier 2021. 
<iframe frameborder="0" width="700" height="300" src="https://data.opendatasoft.com/map/embed/les_arbres_a_paris_et_ses_environs_proches/?&static=false&scrollWheelZoom=false"></iframe>
Ce visuel est une carte. J'ai choisi l'affichage Cluster (Les données sont regroupées, avec une possibilité d'agrégation). Les points ont été mis en verts (petit rappel du thème de la nature). Les chiffres représentent la localisation géographique de l’ensemble des arbres. Grâce à l'utilisation de l'affichage, on peut voir très rapidement la proportion d'arbres présent sur le territoire du Grand Paris. Ces arbres peuvent se trouver dans la rue, dans des parcs, dans des jardins, dans des cimetières et dans des fôrets. Il y a d'importants clusters à l'Ouest et à l'Est. On arrive à distinguer derrière ces gros cluster la présence de fôrets. On peut remarquer que le centre de Paris contient moins d'arbres car il n'y a pas de gros clusters.

Résumé des manipulations sur Opendatasoft : Ajout du jeux de données "Les arbres", modification de l'affichage et de la couleur, enregistrement de la carte, copié/collé du lien Frame.

**2. La vie en vert à Rennes **

Cette carte a été faite sur Opendatasoft. Le jeu de données se nomme _"Arbres d'ornement des espaces verts de la Ville de Rennes"_. La source provient de _Rennes-Metropole_ et a pour producteur la Ville de Rennes.Elle date du 28 Janvier 2021.
J'ai choisi ces données pour comparer rapidement avec le jeu de données des Arbres au sein du Grand Paris.
<iframe frameborder="0" width="700" height="300" src="https://data.opendatasoft.com/map/embed/vegetation_a_rennes/?&static=false&scrollWheelZoom=false"></iframe>

On peut voir qu'il y a peu de gros cluster au sein même de la ville de Rennes. On retrouve une plus importantes part d'abres à l'extérieur de la ville de Rennes. De plus, au sein de Rennes, les clusters sont éloignés les uns des autres. 
Résumé des manipulations : Ajout du jeux de données "Les arbres", modification de l'affichage et de la couleur, enregistrement de la carte, copié/collé du lien Frame.

### Comparaison et analyse 

Après avoir eu une vue d'ensemble de ces deux jeux de données, nous pouvons  observer que l'on retrouve d'importants clusters dans Paris et ses environs comparé à Rennes. 
Cependant, cela est assez logique compte tenu de la superficie différente avec Rennes.
J'ai voulu connaitre la superficie de Paris et de Rennes. Pour se faire, j'ai utilisé l'outils Wiki Data Query Service. 

Ma requête :

````spaql
SELECT ?commune ?communeLabel ?pop ?area ?density
WHERE 
{
  ?commune wdt:P31 wd:Q484170 .
  ?commune wdt:P1082 ?pop .
  ?commune wdt:P2046 ?area 
  FILTER (?pop > 200000)
  BIND( (?pop / ?area) as ?density )
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],fr,en". }
}
ORDER BY DESC(?density)
````
Le résultat montre que la ville de Rennes a une superficie de 50.39 Km2 et que celle de Paris est de 105.40 Km2. Paris est deux fois plus grand que Rennes, ainsi cela ne parait pas sureprenant qu'il y ait 2 fois plus de végétation. Car pour avoir de la végétation, il faut de l'espace. Cependant, Paris et ses alentours proches ont beaucoup d'arbres dispersés dans toute la ville. 

# Visualisation des données : utilisation de l'outils Analyse sur Opendatasoft 

Suite à l'outil Cartes, j'ai voulu découvrir et m'interesser aux endroits où l'on retrouvait des arbres dans le Grand Paris. Pour se faire, j'ai repris le jeu de données de Paris Data. Par la suite, j'ai utilisé l'onglet "Analyse". En Axe Y, j'ai choisi "Moyenne" et pour l'Axe X la catégorie "Domanialité". Ne connaissant pas ce mot, après quelques recherches, je peux traduire ce mot par Domaine Public. Pour l'affichage, je voulais rester dans le thème des arbres avec le graphique "TreeMap", malheureusement celui-ci ne mettait pas en valeur les données. Les deux meilleurs visuels, pour ces données, sont les affichages 'lignes' ou 'camembert'. J'ai pris ce dernier et j'ai également changé les couleurs afin d'opter pour des couleurs plus pastels afin que chaque catégories soient bien visibles.

Voici le rendu du graphique :
<iframe src="https://data.opendatasoft.com/explore/embed/dataset/les-arbres@parisdata/analyze/?disjunctive.typeemplacement&disjunctive.arrondissement&disjunctive.libellefrancais&disjunctive.genre&disjunctive.espece&disjunctive.varieteoucultivar&disjunctive.stadedeveloppement&disjunctive.remarquable&dataChart=eyJxdWVyaWVzIjpbeyJjb25maWciOnsiZGF0YXNldCI6Imxlcy1hcmJyZXNAcGFyaXNkYXRhIiwib3B0aW9ucyI6eyJkaXNqdW5jdGl2ZS50eXBlZW1wbGFjZW1lbnQiOnRydWUsImRpc2p1bmN0aXZlLmFycm9uZGlzc2VtZW50Ijp0cnVlLCJkaXNqdW5jdGl2ZS5saWJlbGxlZnJhbmNhaXMiOnRydWUsImRpc2p1bmN0aXZlLmdlbnJlIjp0cnVlLCJkaXNqdW5jdGl2ZS5lc3BlY2UiOnRydWUsImRpc2p1bmN0aXZlLnZhcmlldGVvdWN1bHRpdmFyIjp0cnVlLCJkaXNqdW5jdGl2ZS5zdGFkZWRldmVsb3BwZW1lbnQiOnRydWUsImRpc2p1bmN0aXZlLnJlbWFycXVhYmxlIjp0cnVlfX0sImNoYXJ0cyI6W3siYWxpZ25Nb250aCI6dHJ1ZSwidHlwZSI6InBpZSIsImZ1bmMiOiJBVkciLCJ5QXhpcyI6ImlkYmFzZSIsInNjaWVudGlmaWNEaXNwbGF5Ijp0cnVlLCJjb2xvciI6InJhbmdlLVNwZWN0cmFsIiwicG9zaXRpb24iOiJjZW50ZXIifV0sInhBeGlzIjoiZG9tYW5pYWxpdGUiLCJtYXhwb2ludHMiOjUwLCJzb3J0IjoiIiwic2VyaWVzQnJlYWtkb3duIjoiIiwic2VyaWVzQnJlYWtkb3duVGltZXNjYWxlIjoiIn1dLCJ0aW1lc2NhbGUiOiIiLCJkaXNwbGF5TGVnZW5kIjp0cnVlLCJhbGlnbk1vbnRoIjp0cnVlfQ%3D%3D&static=false&datasetcard=false" width="400" height="300" frameborder="0"></iframe>


Légende :


_(Dans l'ordre décroissant)_


1.Couleur rouge foncée: 3,4 % = Cimetière 
2. Couleur bleu clair : 7,3% = Périphérique 
3. Couleur bordeau : 7,5% = Alignement _(arbres alignés à la suite les uns des autres)_ 
4. Couleur beige : 10% = DFPE _(Direction des Familles et de la Petite Enfance)_
5. Couleur vert foncé : 11% = Jardin 
6. Couleur orange foncé : 11% = DASCO _(Direction des Affaires Scolaires Collège)_
7. Couleur vert clair : 11.7% = DJS _(Direction de la Jeunesse et des Sports)_
8. Couleur orange clair : 18% = DASES _(Direction de l'Action Sociale de l'Enfance et de la Santé )_
9. Couleur corail : 20,1% = DAC _(Direction des Affaires Culturelles)_


Ma première remarque face à cette analyse est le manque de légende face à ces acronymes. Le lecteur doit faire la recherche ainsi ce n'est pas lisible et compréhensible rapidement. De plus, certains descripteurs sont écrits en majuscules et d'autres en minuscules. Pour les acronymes s'est assez logique mais pour les termes "périphérique" et "cimetière" cela peut penser à une erreur. 

Suite à cette remarque, le point  positif est que dans l'onglet "Informations", il y a un lien qui est mis à disposition pour avoir plus de renseignements. Ce lien renvoie au site de Paris avec pour titre ("L'arbre à Paris")[https://www.paris.fr/pages/l-arbre-a-paris-199]. Il est souvent mise à jour, la dernière datant du 22/01/2021.

Par la suite, lorsque nous avons les informations nécéssaire, on peut voir que la majorité des arbres sont localisés dans des sites culturelles/patrimoniaux mais aussi dans des lieux scolaires ou autres équipements municipaux. Les taux d'arbres dans les jardins ou alignés sont assez faibles au sein du Grand Paris. 


Manipulations faites sur OpendataSoft : Chois des axes et de l'affichage, changements des couleurs, copié/collé du lien Frame.

# Visualisation des données : utilisation de l'outils Open Refine 


Pour finaliser l'exercice j'ai travaillé sur l'outil OpenRefine. Pour se faire, j'ai crée un nouveau projet et importé mon fichier CSV. 
Voici un résumé de mes manipulations. J'avais en tête d'ajouter d'autres informations complémentaires sur le tableau dans OpenRefine, mais par manque de temps et d'expérience, cela n'a pas été possible. 


Manipulations : 
- Téléchargement du fichier CSV.
- Ouverture de facettes textuelles de chaque colonne pour voir les erreurs et modifications possibles.
- Regroupement et fusion dans la colonne "Libellé français". 3 libellés ont pu etre regroupé.
- Pour éviter des mots en majuscules ou en minuscule j'ai ajouté la fonction transformation courante ' majuscules aux initiales' dans la colones "Especes" afin d'harmoniser le tout.
- Reconciliation pour la colonne "Variete oucultivar". Certaines variétés ont pu être retrouvé par Wikidata. 
- Déplacement de la colone 'IDBASE" en dernière position sur le tableau.
- Remplacement du titre de la colonne 'TYPE EMPLACEMENT' par 'SUJET'.
- Ajout partiel de la durée de vie de certains arbres. _(Avec plus d'expérience, j'aurai crée une colonne afin de divisier les cellules multivaluées et donc d'avoir une nouvelle  colonne 'Durée de vie' )_.
- Changement de nom de la colonne "Domanialité" par "Domaine Public".
- Dans la colonne "Domanialité", mise en minuscule des termes "périphérique" et "cimetière".
- Ajout des légendes entre parenthèses pour les acronymes.
- Mise en minuscules avec majuscules aux initiales dans la colonne "Lieu/adresse".
- Tri par ordre alphabétique dans la colonne "Arrondissement"
- Ajout d'étoiles sur les arbres 'Remarquables'. 
- Reconciliation dans la colonne "Arrondissement"
A travers, l'utilisation d'Open Refine, on peut voir qe ce tableau a des soucis de légendes. En effet, on n'avait déjà pu apercevoir que les acronymes n'étaient pas expliqués pour la 'Domanialité'. Là encore, dans la colonne 'Stade en développement', il y a inscrit des lettres 'M', 'JA','J' et 'A'. Cependant aucune légende ne fait office de sous-titres à ces lettres. On peut imaginer que ce sont des mois Mars, Janvier, Juin et Aout. Mais on a aucune certitude et la page de Paris [https://www.paris.fr/pages/l-arbre-a-paris-199] ne donne pas plus d'informations. 

Voici l'historique de Open refine 
````sparql
[
  {
    "op": "core/recon",
    "engineConfig": {
      "facets": [
        {
          "type": "list",
          "name": "LIBELLE FRANCAIS",
          "expression": "value",
          "columnName": "LIBELLE FRANCAIS",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "Abricotier",
                "l": "Abricotier"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "config": {
      "mode": "standard-service",
      "service": "https://wdreconcile.toolforge.org/en/api",
      "identifierSpace": "http://www.wikidata.org/entity/",
      "schemaSpace": "http://www.wikidata.org/prop/direct/",
      "type": {
        "id": "Q811534",
        "name": "remarkable tree"
      },
      "autoMatch": false,
      "columnDetails": [],
      "limit": 0
    },
    "description": "Reconcile cells in column LIBELLE FRANCAIS to type Q811534"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "list",
          "name": "LIBELLE FRANCAIS",
          "expression": "value",
          "columnName": "LIBELLE FRANCAIS",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "Abricotier",
                "l": "Abricotier"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "similarValue": "Abricotier",
    "judgment": "matched",
    "match": {
      "id": "Q16032016",
      "name": "Abricotier",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item Abricotier (Q16032016) for cells containing \"Abricotier\" in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "COMPLEMENT ADRESSE",
    "newColumnName": "MAIRE DES ARRONDISSEMENTS",
    "description": "Rename column COMPLEMENT ADRESSE to MAIRE DES ARRONDISSEMENTS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "REMARQUABLE",
    "expression": "value",
    "edits": [
      {
        "from": [
          "OUI"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Remarquable"
      }
    ],
    "description": "Mass edit cells in column REMARQUABLE"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "expression": "value",
    "edits": [
      {
        "from": [
          "BOIS DE BOULOGNE| Pierre Christophe BAGUET"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "BOIS DE BOULOGNE| Pierre Christophe BAGUET"
      }
    ],
    "description": "Mass edit cells in column ARRONDISSEMENT"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "expression": "value",
    "edits": [
      {
        "from": [
          "BOIS DE BOULOGNE"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "BOIS DE BOULOGNE | Pierre Christophe BAGUET"
      }
    ],
    "description": "Mass edit cells in column ARRONDISSEMENT"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "expression": "value",
    "edits": [
      {
        "from": [
          "BOIS DE VINCENNES"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "BOIS DE VINCENNES | Charlotte LIBERT-ALBANEL"
      }
    ],
    "description": "Mass edit cells in column ARRONDISSEMENT"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "DOMANIALITE",
    "newColumnName": "DOMAINE PUBLIC",
    "description": "Rename column DOMANIALITE to DOMAINE PUBLIC"
  },
  {
    "op": "core/recon",
    "engineConfig": {
      "facets": [
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "VAL-DE-MARNE",
                "l": "VAL-DE-MARNE"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "config": {
      "mode": "standard-service",
      "service": "https://wdreconcile.toolforge.org/en/api",
      "identifierSpace": "http://www.wikidata.org/entity/",
      "schemaSpace": "http://www.wikidata.org/prop/direct/",
      "type": {
        "id": "Q1570417",
        "name": "Arbre"
      },
      "autoMatch": true,
      "columnDetails": [],
      "limit": 0
    },
    "description": "Reconcile cells in column LIBELLE FRANCAIS to type Q1570417"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "DOMAINE PUBLIC",
    "expression": "value",
    "edits": [
      {
        "from": [
          "CIMETIERE"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Cimetière"
      }
    ],
    "description": "Mass edit cells in column DOMAINE PUBLIC"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "DOMAINE PUBLIC",
    "expression": "value",
    "edits": [
      {
        "from": [
          "PERIPHERIQUE"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Périphérique"
      }
    ],
    "description": "Mass edit cells in column DOMAINE PUBLIC"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "DOMAINE PUBLIC",
    "expression": "value",
    "edits": [
      {
        "from": [
          "DAC"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "DAC (Direction des Affaires Culturelles)"
      }
    ],
    "description": "Mass edit cells in column DOMAINE PUBLIC"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "DOMAINE PUBLIC",
    "expression": "value",
    "edits": [
      {
        "from": [
          "DJS"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "DJS (Direction de la Jeunesse et des Sports)"
      }
    ],
    "description": "Mass edit cells in column DOMAINE PUBLIC"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "DOMAINE PUBLIC",
    "expression": "value",
    "edits": [
      {
        "from": [
          "DASCO"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "DASCO (Direction des Affaires Scolaires Collèges)"
      }
    ],
    "description": "Mass edit cells in column DOMAINE PUBLIC"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "DOMAINE PUBLIC",
    "expression": "value",
    "edits": [
      {
        "from": [
          "DFPE"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "DFPE (Direction des Familles et de la Petite Enfance)"
      }
    ],
    "description": "Mass edit cells in column DOMAINE PUBLIC"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "DOMAINE PUBLIC",
    "expression": "value",
    "edits": [
      {
        "from": [
          "DASES"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "DASES (Direction de l'Action Sociale de l'Enfance et de la Santé )"
      }
    ],
    "description": "Mass edit cells in column DOMAINE PUBLIC"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "REMARQUABLE",
    "expression": "value",
    "edits": [
      {
        "from": [
          "NON"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Non"
      }
    ],
    "description": "Mass edit cells in column REMARQUABLE"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Abricotier"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Abricotier|40-45 ans "
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Abelia"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Abelia| 50-100 ans"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Abricotier fruit"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Abricotier"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Ailante"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Ailante| 50 ans"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Alisier"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Alisier| 250 ans"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Althéa"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Althéa| 30-50 ans"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Amandier"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Amandier| 50-80 ans"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Araucaria"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Araucaria| 10-15 ans "
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Arbousier"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Arbousier| 100-400 ans"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Arbre à miel"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Arbre à miel| 35-40 ans"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Argousier"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Argousier| 80 ans"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/column-removal",
    "columnName": "MAIRE DES ARRONDISSEMENTS",
    "description": "Remove column MAIRE DES ARRONDISSEMENTS"
  },
  {
    "op": "core/column-removal",
    "columnName": "NUMERO",
    "description": "Remove column NUMERO"
  },
  {
    "op": "core/text-transform",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIEU / ADRESSE",
    "expression": "value.toTitlecase()",
    "onError": "keep-original",
    "repeat": false,
    "repeatCount": 10,
    "description": "Text transform on cells in column LIEU / ADRESSE using expression value.toTitlecase()"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Abricotier"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Abricotier|40-45 ans"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "LIBELLE FRANCAIS",
    "expression": "value",
    "edits": [
      {
        "from": [
          "Abricotier|40-45 ans ",
          "Abricotier|40-45 ans"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Abricotier|40-45 ans "
      },
      {
        "from": [
          "Troene",
          "Troëne"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Troene"
      },
      {
        "from": [
          "Aubépine",
          "Aubepine"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Aubépine"
      }
    ],
    "description": "Mass edit cells in column LIBELLE FRANCAIS"
  },
  {
    "op": "core/text-transform",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ESPECE",
    "expression": "value.toTitlecase()",
    "onError": "keep-original",
    "repeat": false,
    "repeatCount": 10,
    "description": "Text transform on cells in column ESPECE using expression value.toTitlecase()"
  },
  {
    "op": "core/recon",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "config": {
      "mode": "standard-service",
      "service": "https://wdreconcile.toolforge.org/en/api",
      "identifierSpace": "http://www.wikidata.org/entity/",
      "schemaSpace": "http://www.wikidata.org/prop/direct/",
      "type": {
        "id": "Q16521",
        "name": "taxon"
      },
      "autoMatch": true,
      "columnDetails": [],
      "limit": 0
    },
    "description": "Reconcile cells in column VARIETE OUCULTIVAR to type Q16521"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Euchlora''",
    "judgment": "matched",
    "match": {
      "id": "Q17125306",
      "name": "Euchlora",
      "types": [
        "Q16521"
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item Euchlora (Q17125306) for cells containing \"''Euchlora''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Baumannii''",
    "judgment": "matched",
    "match": {
      "id": "Q15344322",
      "name": "Oroya baumannii",
      "types": [
        "Q16521"
      ],
      "score": 75
    },
    "shareNewTopics": false,
    "description": "Match item Oroya baumannii (Q15344322) for cells containing \"''Baumannii''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Elsrijk''",
    "judgment": "matched",
    "match": {
      "id": "Q4673145",
      "name": "Acer campestre 'Elsrijk'",
      "types": [
        "Q4886"
      ],
      "score": 48
    },
    "shareNewTopics": false,
    "description": "Match item Acer campestre 'Elsrijk' (Q4673145) for cells containing \"''Elsrijk''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Pissardii''",
    "judgment": "matched",
    "match": {
      "id": "Q146951",
      "name": "Prunus cerasifera",
      "types": [
        "Q16521"
      ],
      "score": 72
    },
    "shareNewTopics": false,
    "description": "Match item Prunus cerasifera (Q146951) for cells containing \"''Pissardii''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Caucasica''",
    "judgment": "matched",
    "match": {
      "id": "Q12217305",
      "name": "Iris caucasica",
      "types": [
        "Q16521"
      ],
      "score": 78
    },
    "shareNewTopics": false,
    "description": "Match item Iris caucasica (Q12217305) for cells containing \"''Caucasica''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Atropurpureum''",
    "judgment": "matched",
    "match": {
      "id": "Q17281507",
      "name": "Bryum atropurpureum",
      "types": [
        "Q16521"
      ],
      "score": 81
    },
    "shareNewTopics": false,
    "description": "Match item Bryum atropurpureum (Q17281507) for cells containing \"''Atropurpureum''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Nanguen'' LUTECE",
    "judgment": "matched",
    "match": {
      "id": "Q7879317",
      "name": "Ulmus 'Nanguen' = Lutece",
      "types": [
        "Q4886"
      ],
      "score": 82
    },
    "shareNewTopics": false,
    "description": "Match item Ulmus 'Nanguen' = Lutece (Q7879317) for cells containing \"''Nanguen'' LUTECE\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "expression": "value",
    "edits": [
      {
        "from": [
          "BOIS DE BOULOGNE | Pierre Christophe BAGUET"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "BOIS DE BOULOGNE"
      }
    ],
    "description": "Mass edit cells in column ARRONDISSEMENT"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "expression": "value",
    "edits": [
      {
        "from": [
          "BOIS DE VINCENNES | Charlotte LIBERT-ALBANEL"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "BOIS DE VINCENNES"
      }
    ],
    "description": "Mass edit cells in column ARRONDISSEMENT"
  },
  {
    "op": "core/column-move",
    "columnName": "IDBASE",
    "index": 14,
    "description": "Move column IDBASE to position 14"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "TYPE EMPLACEMENT",
    "newColumnName": "SUJET",
    "description": "Rename column TYPE EMPLACEMENT to SUJET"
  },
  {
    "op": "core/text-transform",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "VARIETE OUCULTIVAR",
          "expression": "value",
          "columnName": "VARIETE OUCULTIVAR",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PLATANOR®",
                "l": "PLATANOR®"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "expression": "value.toTitlecase()",
    "onError": "keep-original",
    "repeat": false,
    "repeatCount": 10,
    "description": "Text transform on cells in column VARIETE OUCULTIVAR using expression value.toTitlecase()"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "VARIETE OUCULTIVAR",
          "expression": "value",
          "columnName": "VARIETE OUCULTIVAR",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "''Zlatia''",
                "l": "''Zlatia''"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Zlatia''",
    "judgment": "matched",
    "match": {
      "id": "Q93015927",
      "name": "Fagus sylvatica f. zlatia",
      "types": [
        "Q16521"
      ],
      "score": 40
    },
    "shareNewTopics": false,
    "description": "Match item Fagus sylvatica f. zlatia (Q93015927) for cells containing \"''Zlatia''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "VARIETE OUCULTIVAR",
          "expression": "value",
          "columnName": "VARIETE OUCULTIVAR",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "''Youngii''",
                "l": "''Youngii''"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Youngii''",
    "judgment": "matched",
    "match": {
      "id": "Q15566088",
      "name": "Cissus youngii",
      "types": [
        "Q16521"
      ],
      "score": 67
    },
    "shareNewTopics": false,
    "description": "Match item Cissus youngii (Q15566088) for cells containing \"''Youngii''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "VARIETE OUCULTIVAR",
          "expression": "value",
          "columnName": "VARIETE OUCULTIVAR",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "''Winter Gold''",
                "l": "''Winter Gold''"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Winter Gold''",
    "judgment": "matched",
    "match": {
      "id": "Q104182888",
      "name": "Eremophila ‘Winter Gold’",
      "types": [
        "Q16521"
      ],
      "score": 67
    },
    "shareNewTopics": false,
    "description": "Match item Eremophila ‘Winter Gold’ (Q104182888) for cells containing \"''Winter Gold''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "VARIETE OUCULTIVAR",
          "expression": "value",
          "columnName": "VARIETE OUCULTIVAR",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "''Wanoux'' VADA",
                "l": "''Wanoux'' VADA"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Wanoux'' VADA",
    "judgment": "matched",
    "match": {
      "id": "Q7879355",
      "name": "Ulmus 'Wanoux' = Vada",
      "types": [
        "Q4886"
      ],
      "score": 79
    },
    "shareNewTopics": false,
    "description": "Match item Ulmus 'Wanoux' = Vada (Q7879355) for cells containing \"''Wanoux'' VADA\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "VARIETE OUCULTIVAR",
          "expression": "value",
          "columnName": "VARIETE OUCULTIVAR",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "''Vossii''",
                "l": "''Vossii''"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Vossii''",
    "judgment": "matched",
    "match": {
      "id": "Q149857",
      "name": "Aloe vossii",
      "types": [
        "Q16521"
      ],
      "score": 71
    },
    "shareNewTopics": false,
    "description": "Match item Aloe vossii (Q149857) for cells containing \"''Vossii''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "VARIETE OUCULTIVAR",
          "expression": "value",
          "columnName": "VARIETE OUCULTIVAR",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "''Schwedleri''",
                "l": "''Schwedleri''"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''Schwedleri''",
    "judgment": "matched",
    "match": {
      "id": "Q9579167",
      "name": "Acer schwedleri",
      "types": [
        "Q16521"
      ],
      "score": 80
    },
    "shareNewTopics": false,
    "description": "Match item Acer schwedleri (Q9579167) for cells containing \"''Schwedleri''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/text-transform",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "expression": "value.toTitlecase()",
    "onError": "keep-original",
    "repeat": false,
    "repeatCount": 10,
    "description": "Text transform on cells in column VARIETE OUCULTIVAR using expression value.toTitlecase()"
  },
  {
    "op": "core/recon",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "config": {
      "mode": "standard-service",
      "service": "https://wdreconcile.toolforge.org/en/api",
      "identifierSpace": "http://www.wikidata.org/entity/",
      "schemaSpace": "http://www.wikidata.org/prop/direct/",
      "type": {
        "id": "Q252916",
        "name": "administrative quarter of Paris"
      },
      "autoMatch": true,
      "columnDetails": [],
      "limit": 0
    },
    "description": "Reconcile cells in column ARRONDISSEMENT to type Q252916"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "BOIS DE VINCENNES",
    "judgment": "matched",
    "match": {
      "id": "Q271639",
      "name": "bois de Vincennes",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item bois de Vincennes (Q271639) for cells containing \"BOIS DE VINCENNES\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "HAUTS-DE-SEINE",
                "l": "HAUTS-DE-SEINE"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "HAUTS-DE-SEINE",
    "judgment": "matched",
    "match": {
      "id": "Q12543",
      "name": "Hauts-de-Seine",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item Hauts-de-Seine (Q12543) for cells containing \"HAUTS-DE-SEINE\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "HAUTS-DE-SEINE",
                "l": "HAUTS-DE-SEINE"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''fastigiata''",
    "judgment": "matched",
    "match": {
      "id": "Q15227127",
      "name": "Carex fastigiata",
      "types": [
        "Q16521"
      ],
      "score": 77
    },
    "shareNewTopics": false,
    "description": "Match item Carex fastigiata (Q15227127) for cells containing \"''fastigiata''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 10E ARRDT",
                "l": "PARIS 10E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 10E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q163948",
      "name": "10th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 10th arrondissement of Paris (Q163948) for cells containing \"PARIS 10E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 11E ARRDT",
                "l": "PARIS 11E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 11E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q169293",
      "name": "11th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 11th arrondissement of Paris (Q169293) for cells containing \"PARIS 11E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 12E ARRDT",
                "l": "PARIS 12E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 12E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q171689",
      "name": "12th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 12th arrondissement of Paris (Q171689) for cells containing \"PARIS 12E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 13E ARRDT",
                "l": "PARIS 13E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 13E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q175129",
      "name": "13th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 13th arrondissement of Paris (Q175129) for cells containing \"PARIS 13E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 13E ARRDT",
                "l": "PARIS 13E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''erecta''",
    "judgment": "matched",
    "match": {
      "id": "Q11273546",
      "name": "Ficus erecta",
      "types": [
        "Q16521"
      ],
      "score": 67
    },
    "shareNewTopics": false,
    "description": "Match item Ficus erecta (Q11273546) for cells containing \"''erecta''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 14E ARRDT",
                "l": "PARIS 14E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 14E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q187153",
      "name": "14th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 14th arrondissement of Paris (Q187153) for cells containing \"PARIS 14E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 15E ARRDT",
                "l": "PARIS 15E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 15E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q191066",
      "name": "15th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 15th arrondissement of Paris (Q191066) for cells containing \"PARIS 15E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 16E ARRDT",
                "l": "PARIS 16E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 16E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q194420",
      "name": "16th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 16th arrondissement of Paris (Q194420) for cells containing \"PARIS 16E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 17E ARRDT",
                "l": "PARIS 17E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 17E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q197297",
      "name": "17th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 17th arrondissement of Paris (Q197297) for cells containing \"PARIS 17E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 17E ARRDT",
                "l": "PARIS 17E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''italica''",
    "judgment": "matched",
    "match": {
      "id": "Q8068164",
      "name": "Zea italica",
      "types": [
        "Q16521"
      ],
      "score": 78
    },
    "shareNewTopics": false,
    "description": "Match item Zea italica (Q8068164) for cells containing \"''italica''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 18E ARRDT",
                "l": "PARIS 18E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 18E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q200126",
      "name": "18th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 18th arrondissement of Paris (Q200126) for cells containing \"PARIS 18E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 19E ARRDT",
                "l": "PARIS 19E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 19E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q204622",
      "name": "19th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 19th arrondissement of Paris (Q204622) for cells containing \"PARIS 19E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 1ER ARRDT",
                "l": "PARIS 1ER ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 1ER ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q161741",
      "name": "1st arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 1st arrondissement of Paris (Q161741) for cells containing \"PARIS 1ER ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 1ER ARRDT",
                "l": "PARIS 1ER ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "VARIETE OUCULTIVAR",
    "similarValue": "''fastigiata''",
    "judgment": "matched",
    "match": {
      "id": "Q15227127",
      "name": "Carex fastigiata",
      "types": [
        "Q16521"
      ],
      "score": 77
    },
    "shareNewTopics": false,
    "description": "Match item Carex fastigiata (Q15227127) for cells containing \"''fastigiata''\" in column VARIETE OUCULTIVAR"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 20E ARRDT",
                "l": "PARIS 20E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 20E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q210720",
      "name": "20th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 20th arrondissement of Paris (Q210720) for cells containing \"PARIS 20E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 2E ARRDT",
                "l": "PARIS 2E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 2E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q209549",
      "name": "2nd arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 2nd arrondissement of Paris (Q209549) for cells containing \"PARIS 2E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 3E ARRDT",
                "l": "PARIS 3E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 3E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q223140",
      "name": "3rd arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 3rd arrondissement of Paris (Q223140) for cells containing \"PARIS 3E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 4E ARRDT",
                "l": "PARIS 4E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 4E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q230127",
      "name": "4th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 4th arrondissement of Paris (Q230127) for cells containing \"PARIS 4E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 5E ARRDT",
                "l": "PARIS 5E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 5E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q238723",
      "name": "5th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 5th arrondissement of Paris (Q238723) for cells containing \"PARIS 5E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 6E ARRDT",
                "l": "PARIS 6E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 6E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q245546",
      "name": "6th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 6th arrondissement of Paris (Q245546) for cells containing \"PARIS 6E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 7E ARRDT",
                "l": "PARIS 7E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 7E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q259463",
      "name": "7th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 7th arrondissement of Paris (Q259463) for cells containing \"PARIS 7E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 8E ARRDT",
                "l": "PARIS 8E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 8E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q270230",
      "name": "8th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 8th arrondissement of Paris (Q270230) for cells containing \"PARIS 8E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "PARIS 9E ARRDT",
                "l": "PARIS 9E ARRDT"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "PARIS 9E ARRDT",
    "judgment": "matched",
    "match": {
      "id": "Q275118",
      "name": "9th arrondissement of Paris",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item 9th arrondissement of Paris (Q275118) for cells containing \"PARIS 9E ARRDT\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "SEINE-SAINT-DENIS",
                "l": "SEINE-SAINT-DENIS"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "SEINE-SAINT-DENIS",
    "judgment": "matched",
    "match": {
      "id": "Q12761",
      "name": "Seine-Saint-Denis",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item Seine-Saint-Denis (Q12761) for cells containing \"SEINE-SAINT-DENIS\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "list",
          "name": "ARRONDISSEMENT",
          "expression": "value",
          "columnName": "ARRONDISSEMENT",
          "invert": false,
          "omitBlank": false,
          "omitError": false,
          "selection": [
            {
              "v": {
                "v": "VAL-DE-MARNE",
                "l": "VAL-DE-MARNE"
              }
            }
          ],
          "selectBlank": false,
          "selectError": false
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ARRONDISSEMENT",
    "similarValue": "VAL-DE-MARNE",
    "judgment": "matched",
    "match": {
      "id": "Q12788",
      "name": "Val-de-Marne",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item Val-de-Marne (Q12788) for cells containing \"VAL-DE-MARNE\" in column ARRONDISSEMENT"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "LIBELLE FRANCAIS: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "LIBELLE FRANCAIS",
          "from": 35.5,
          "to": 36.5,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        },
        {
          "type": "range",
          "name": "ARRONDISSEMENT: best candidate's score",
          "expression": "cell.recon.best.score",
          "columnName": "ARRONDISSEMENT",
          "from": 24,
          "to": 80,
          "selectNumeric": true,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "ESPECE",
    "expression": "value",
    "edits": [
      {
        "from": [
          "N. Sp."
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "Non spécifié "
      }
    ],
    "description": "Mass edit cells in column ESPECE"
  }
]
````

# Conclusion

Pour conclure, l'utilisation de plusieurs outils et types d'affichages m'a permi de découvrir en profondeur les informtaions du jeux de données choisi. J'ai pu voir des informations intéressantes mais aussi des problèmes qui ont pu être modifié par la suite grâce à l'outil OpenRefine. 







