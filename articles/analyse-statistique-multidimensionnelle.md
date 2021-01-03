**Les informations présentées ici sont des extraits de cours ou de présentations :**
  
[Statistique Descriptive Multidimensionnelle, Alain Baccini](https://www.math.univ-toulouse.fr/~baccini/zpedago/asdm.pdf)   
[ACP et nuage des points-variables, Jean-Yves BAUDOT](http://www.jybaudot.fr/Analdonnees/cerclecor.html)      
[Positionnement multidimensionnel (MDS), Philippe BESSE](https://www.math.univ-toulouse.fr/~besse/Wikistat/pdf/st-m-explo-mds.pdf)   
[L’Analyse des Correspondances Multiples (ACM), Marie Chavent](http://www.math.u-bordeaux.fr/~mchave100p/wordpress/wp-content/uploads/2013/10/ACM.pdf)  
[Décomposition en valeurs singulières (SVD), UFR MIME](https://beedotkiran.github.io/MLcourse_Lille3/ML_Cours_04_SVD.pdf)

J'ai fait également un tutoriel sur la mise en œuvre de l'analyse statistique multidimensionnelle avec Python. Il est disponible [ici](https://github.com/fayeab/python-data-science/blob/main/tutoriels/python-analyse-statistique-multidimensionnelle.ipynb) 

# Analyse Statistique Multidimensionnelle

- Analyse en composantes principales (ACP)  
- Analyses factorielles (AFC)
- Analyses des correspondances multiples (ACM)
- Décomposition en valeurs singulière (SVD)  
- Positionnement multidimensionnel (MDS)   

## [A. Analyse en composantes principales (ACP)](https://www.math.univ-toulouse.fr/~baccini/zpedago/asdm.pdf)

Le principe général de l'ACP. est de réduire la dimension des données initiales (qui est `p` si l'on considère `p` variables quantitatives), en remplaçant les `p` variables initiales par `q` facteurs appropriés (`q` < `p`).
Les données, toujours centrées, doivent en plus être réduites lorsque les variables sont hétérogènes.
Les `q` facteurs cherchés sont des moyennes pondérées des variables initiales. Leur choix se fait en maximisant la dispersion des individus selon ces facteurs (autrement dit, les facteurs retenus doivent ˆetre de variance maximum). 
Des techniques mathématiques appropiées permettent de réaliser tout cela de façon automatique et optimale.

###  [1. Résultats sur les variables](https://www.math.univ-toulouse.fr/~baccini/zpedago/asdm.pdf)

La technique de l'ACP. permet de calculer les corrélations variables-facteurs, autrement dit les coefficients de corr´elation linéaire entre chaque variable initiale et chaque facteur retenu.
Dans un premier temps, ces quantités permettent un début d’interprétation des facteurs, dans la mesure où elles indiquent comment ils sont liés aux variables initiales. A ce stade, il est recommandé
d'utiliser aussi la matrice des corrélations entre variables initiales, pour compléter cette interprétation.  
Dans un second temps, les corrélations variables-facteurs permettent de réaliser les graphiques
des variables dont l'étude d´etaillée conduit à  préciser la signification des axes, c'est-à -dire des facteurs. On doit considérer uniquement le graphique selon les axes 1 et 2 si l'on a choisi `q `= 2; on doit au contraire considérer les 3 graphiques selon les axes 1 et 2, 1 et 3, 2 et 3, si l'on a choisi `q` = 3.

### [2. Résultats sur les individus](https://www.math.univ-toulouse.fr/~baccini/zpedago/asdm.pdf)

Là  encore, la technique de l'ACP permet de calculer les coordonnées des individus sur les axes, leurs contributions à la dispersion selon chacun de ces axes (ainsi que leurs contributions à la dispersion globale, selon les `p` dimensions) et les cosinus carrés.
Les coordonnées permettent de réaliser les graphiques des individus (1 ou 3 graphiques, selon que l’on a choisi `q` = 2 ou `q` = 3). Concernant ces graphiques, il faut tout d'abord noter que leurs axes s'interprétent de la mˆeme manière que les axes des graphiques des variables : les uns comme les autres sont associ´es aux facteurs.
En associant à ces graphiques les contributions des individus aux axes, on peut affiner l'interprétation de ces axes : chacun d'entre eux est surtout déterminé par les quelques individus présentant les plus fortes contributions; ce sont en g´en´eral ceux situ´es en position extrême sur l'axe, c’est-à-dire y ayant les plus fortes coordonnées, soit positives soit négatives. Bien sur, avant d'utiliser un tel individu pour affiner l'interprétation d’un axe, il faut s'assurer que cet individu est bien repr´esenté sur cet axe, autrement dit que le cosinus carré correspondant est grand (proche de 1).

###  [3. Cercle de corrélation](http://www.jybaudot.fr/Analdonnees/cerclecor.html)

Si une variable devait être parfaitement corrélée avec l’axe F1, sa représentation se confondrait avec lui (point rouge ci-dessous). Cette situation ne se vérifie presque jamais. Si l’inertie d’une variable est complètement absorbée par les deux premières composantes principales, le point se trouve sur le cercle mais entre les deux axes F1 et F2 (point bleu). Si la corrélation est parfaite mais qu’elle est négative, par exemple avec la première composante, il se trouve sur un autre quart du cercle (point vert). Si l’inertie de la variable n’est presque pas absorbée par les deux premiers axes mais par un troisième ou par les suivants, non représentés, son point représentatif est assez loin du cercle, du moins dans le premier plan factoriel. Ceci signifie que la corrélation est faible et que cette variable ne doit pas être prise en compte à ce niveau-ci de l’analyse (point rose).
<img src="images/analyse-multivariee/cercle_correlation.png">

## [B. Analyses factorielles (AFC)](https://www.math.univ-toulouse.fr/~baccini/zpedago/asdm.pdf)

L'AFC est une ACP particulière. On réalise l'ACP du tableau des profils-lignes (les individus de cette ACP sont les lignes de la table de contingence, c’est-à-dire les modalités de `X`) et l'on fait la représentation graphique
des individus, donc des modalités de `X` (dans cette ACP particulière, on ne s'intéresse pas au graphique des variables). On a un seul graphique si on ne conserve que deux dimensions, plusieurs dans le cas contraire.
On réalise d'autre part l'ACP du tableau des profils-colonnes (les individus de cette ACP sont maintenant les colonnes de la table de contingence, c'est-à-dire les modalités de `Y` ) et l'on fait la représentation graphique des individus, donc des modalités de `Y`. On montre que ces deux ACP se correspondent (ce qui est normal, puisque leurs données sont extraites de la même table de contingence) et qu'il est donc l'egitime de superposer les deux représentations graphiques. On obtient ainsi un graphique de type nuage de points (ou un ensemble de graphiques si on conserve plus de deux dimensions), représentant à la fois les modalités de `X` et celles de `Y` . En particulier, on s’attache à étudier les correspondances entre les modalités de `X` et celles de `Y` , d'où le nom de la méthode.


### [Tableau de contingence](https://fr.wikipedia.org/wiki/Tableau_de_contingence)

Un tableau de contingence est une méthode de représentation de données issues d’un comptage permettant d'estimer la dépendance entre deux caractères. Elle consiste à croiser deux caractères d'une population (par exemple une classe d'âge et un score) en dénombrant l'effectif correspondant à la conjonction « caractère 1 » et « caractère 2 ».

Les effectifs partiels sont rassemblés dans un tableau à double entrée, par ligne pour le premier caractère, et par colonne en fonction du second caractère : c'est le « tableau de contingence ».

## [Analyses des correspondances multiples (ACM)](http://www.math.u-bordeaux.fr/~mchave100p/wordpress/wp-content/uploads/2013/10/ACM.pdf)


Il s’agit d’une méthode de description statistique multidimensionelle d'un tableau de données qualitatives. Comme l'ACP pour les données quantitatives, elle permet pour des données qualitatives :
* des représentations graphiques du contenu du tableau de donn´ees : représentation des "similitudes" entre les individus et entre les modalités des variables qualitatives.
* un recodage en données numériques, sur lesquelles on peut ensuite appliquer d'autres méthodes (par exemple des algorithmes de classification).

En pratique, l’ACM est une AFC appliquée au tableau disjonctif complet c’est à dire à la matrice des indicatrices des modalités des variables qualitatives.

Si les données regroupent des variables qualitatives et quantitatives, il faudra effectuer recodage en classes (discrétisation) des variables quantitative avant de passer à une analyse factorielle multiple des correspondances. 

**Remarque** : il ne serait pas très compliqué de recalculer directement les composantes de l'ACM à partir de la SVD du tableau disjonctif complet est obtenu en remplaçant chaque variables par les indicatrices (dummy variables) de ses modalités.

L'ACM peut être aussi vue comme une technique de transformation de variables. Elle permet de passer d'un espace discret, décrit par les variables originales, en un espace continu, décrit par les axes factoriels. Sans perte d'informations si l'on choisit de conserver tous les axes. Avec une perte d'information contrôlée lorsque l'on ne conserve que les premiers axes. En effet, les derniers facteurs traduisent essentiellement les fluctuations aléatoires dues à l'échantillonnage, on lisse ainsi les données en nous concentrant sur les informations essentielles.

### [Tableau disjonctif complet](https://fr.wikipedia.org/wiki/Tableau_disjonctif_complet)

Un tableau disjonctif complet (TDC) est un type de représentation de données qualitatives utilisé en analyse des données. Dans ce tableau, une variable qualitative à `K` modalités est remplacée par `K` variables binaires, chacune correspondant à une des modalités.

### [Tableau de Burt](https://fr.wikipedia.org/wiki/Table_de_Burt)

Une table de Burt, (on parle aussi de tableau de Burt) est un type de représentation de données qualitatives utilisé en analyse des données notamment lors d'une AFC ou une ACM. Cette représentation doit son nom à Sir Cyril Lodowic Burt.

Une table de Burt est une matrice carrée symétrique. Elle contient tous les tableaux de contingence des variables prises deux à deux. Elle peut être calculée à partir du tableau disjonctif complet : si l'on note `D` le tableau disjonctif complet, alors la table de Burt `B` est égale à `D`<sup>T</sup>`D`.

## [Décomposition en valeurs singulière (SVD)](https://beedotkiran.github.io/MLcourse_Lille3/ML_Cours_04_SVD.pdf)

La Décomposition en valeur singulière ou SVD (Singular Value Decomposition) est motiver par deux opérations souvent fait dans l'analyse des données :
* Découplage : Séparation dans les composantes indépendantes pour faciliter analyse
* Triage : Ordonnancements de contributions par leur importance ou capacité d'explication

### Décomposition SVD

`A` est une matrice de taille `n×d`, il existe une décomposition `A = UΣV`<sup>T</sup> 

* Le SVD est une manière de factoriser une matrice non-carré qui généralise l’opération de décomposition en valeurs propres (pour une matrice symétrique)
* La troncation des valeurs singulières produit des approximation de bas-rang d’une matrice d’entrée.
* Le rang d’un matrice est les nombres des valeurs singulières non-nul. 
* Les matrices `U` et `V` sont orthogonales et unitaire : il préserve les distances entres les vecteurs de `A`.
* La décomposition SVD pour une matrice non-carrée est unique

### Applications

* Réduction de dimensionnalité (ACP) : Factorisation, traitement de données et d’images, ...
* Compression et de-bruitage par calcul de rang des données.
* Calcul de similarités pour les systèmes de recommandation
* Évaluation d’inverse d’une matrice arbitraire non carrée (pseudo-inverse)
* Analyse des transformations linéaire et systèmes linéaires

# [Positionnement multidimensionnel](https://www.math.univ-toulouse.fr/~besse/Wikistat/pdf/st-m-explo-mds.pdf)
<a id='mds' />

L’objectif du positionnement multidimensionnel (multidimensional scaling, ou MDS, ou ACP d’un tableau de distances) est de construire, à partir de cette matrice, une représentation euclidienne des individus dans un espace de dimension réduite q qui approche au “mieux” les indices observés. Autrement dit, visuellement le graphique obtenu représente en dimension (en général) 2 la meilleure approximation des distances observées entre les individus.
