##  LA VIE EN VERT !



# Introduction
Cette page Github a été créé par moi-même (Alexandra Renard) lors du Master 2 DEFI pour l'examen final du cours de Datavisualition de Monsieur Courtin. 
Comme souvent répété en cours, le plus important ce sont le thème choisi et les jeux de données. J'ai eu du mal à trouver des jeux de données car soit ils étaient compliqués à utiliser soit ils n'étaient pas à mon goût (thématique). Après de nombreuses recherches, sur [data.gouv.fr](https://www.data.gouv.fr/fr/), [data.culture](https://data.culture.gouv.fr/pages/home/) et [Opendatasoft](https://www.opendatasoft.com/fr/), j'ai finalement trouvé, sur ce dernier, un jeux de données.

Après avoir choisi un jeu de données sur "les arbres" , je me suis dirigée vers le sujet autour de la végétation parisienne et rennaise. 

![alt tag](https://user-images.githubusercontent.com/77047183/106200477-54876180-61b7-11eb-87c2-9b2808cc96c5.jpg)

_Source: Un projet de réaménagement des Champs-Elysées est à l’étude. Il prévoit de faire une large place aux jardins et à la végétation. PCA-STREAM, Le Parisien, 11 Janvier 2021_ Lien : https://www.leparisien.fr/paris-75/paris-anne-hidalgo-promet-un-jardin-extraordinaire-sur-les-champs-elysees-11-01-2021-8418444.php


# Visualisation des données : utilisation de l'outils Cartes sur Opendatasoft

**1. La vie en vert au sein du Grand Paris **

Pour commencer à aborder ce sujet, j'ai fait le choix d'avoir une vie d'ensemble de ces données en utilisant l'outil Carte sur Opendatasoft. 
Nous allons débuter par observer la végétation dans la ville de Paris. Le jeu de données choisi se nomme "Les arbres. 
La source est [https://opendata.paris.fr/explore/dataset/les-arbres/information/?disjunctive.typeemplacement&disjunctive.arrondissement&disjunctive.libellefrancais&disjunctive.genre&disjunctive.espece&disjunctive.varieteoucultivar&disjunctive.stadedeveloppement&disjunctive.remarquable](ParisData) et le producteur est la _Direction des Espaces Verts et de l'Environnement - Ville de Paris_. Ce jeu de donnée a pour objectif de montrer l'ensemble des arbres présents à Paris et dans ses envrions proches (Grand Paris). Les données datent du 22 Janvier 2021. 
<iframe frameborder="0" width="700" height="300" src="https://data.opendatasoft.com/map/embed/les_arbres_a_paris_et_ses_environs_proches/?&static=false&scrollWheelZoom=false"></iframe>
Ce visuel est une carte. J'ai choisi l'affichage Cluster (Les données sont regroupées, avec une possibilité d'agrégation). Les points ont été mis en verts (petit rappel de la nature). Les chiffres representent la localisation géographique de l’ensemble des arbres. Grâce à l'utilisation de l'affichage, on peut voir très rapidement la proportion d'arbres présent sur le territoire du Grand Paris. Ces arbres peuvent se trouver dans la rue, dans des parcs, dans des jardins, dans des cimetières et dans des fôrets.

Résumé des manipulations : Ajout du jeux de données "Les arbres", modification de l'affichage et de la couleur.

**2. La vie en vert à Rennes **

Cette carte a été faite sur Opendatasoft. Le jeu de données se nomme _"Arbres d'ornement des espaces verts de la Ville de Rennes"_. La source provient de _Rennes-Metropole_ et a pour producteur la Ville de Rennes.Elle date du 28 Janvier 2021.
<iframe frameborder="0" width="700" height="300" src="https://data.opendatasoft.com/map/embed/vegetation_a_rennes/?&static=false&scrollWheelZoom=false"></iframe>

Résumé des manipulations : Ajout du jeux de données "Les arbres", modification de l'affichage et de la couleur.

### Comparaison et analyse 

Après avoir eu une vue d'ensemble de ces deux jeux de données, nous pouvons voir observer que l'on retrouve d'important clusters dans Paris et ses environs. 
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
Le résultat montre que la ville de Rennes a une superficie de 50.39 Km2 et que celle de Paris est de 105.40 Km2. Paris est deux fois plus grand que Rennes, ainsi cela ne parait pas sureprenant qu'il y ait 2 fois plus de végétation. Car pour avoir de la végétation, il faut de l'espace.

# Visualisation des données : utilisation de l'outils Analyse sur Opendatasoft 

Suite à l'outil Cartes, j'ai voulu découvrir et m'interesser aux endroits où l'on retrouvait des arbres dans le Grand Paris. POur ce faire j'ai repris le jeux de données de Paris Data. Par la suite, j'ai utilisé l'onglet "Analyse". En Axe Y, j'ai choisi "Moyenne" et pour l'Axe X la catégorie "Domanialité". Ne connaissant pas ce mot, après quelques recherches, je peux traduire ce mot par Domaine Public. Pour l'affichage, je voulais rester dans le thème des arbres avec le graphique "TreeMap",malheureusment celui ci ne mettait pas en valeur les données. Les deux meilleurs visiuels, pour ces données, sont l'affichage 'lignes' ou 'camembert'. J'ai également changé les couleurs afin d'opter pour des couleurs plus pastels afin que chaque catégories soient bien visibles.

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
9. Couleur corail : 20,1% = DAC 


Ma première remarque face à cette analyse est le manque de légende face à ces acronymes. Le lecteur doit faire la recherche ainsi ce n'est pas lisible et compréhensible rapidement. 

# Visualisation des données : utilisation de l'outils Open REfine 

Manipulations : 
- Ajout la durée de vie des arbres. 
- Changement de nom de la colonne "Dominialité" par "Domaine Public".
- Dans l'onglet Grouper et éditer j'ai tenté de voir si je pouvais regrouper des informations. Cependant Open Refine n'avait aucune proposition à me faire. 

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block



## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/AlexandraRenard/ExamenDataviz/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
