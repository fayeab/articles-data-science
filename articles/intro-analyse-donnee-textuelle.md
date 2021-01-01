# Introduction à l'analyse de la donnée textuelle

L'objectif est faire une revue des méthodologies relatives au traitement de la donnée textuelle :

* **Préprocessing**
* **Représentation vectorielle des documents**
* **Analyse sémantique latente**
* **Topic modeling**
* **Quelques cas d'usage**

## A. Préprocessing

Le préprocessing est une étape préalable, indispensable et spécifique à l'analyse textuelle. Même si une grosse partie se fait « à la main », il existe néanmoins une méthodologie classique :

1. Tokenisation
   * Mots, n-gram


2. Nettoyage des données
  * Epuration
  * Filtres phonétiques
  * Stemming 
  * Lemmatisation
  * Synomisation
  *  Part of Speech (POS) tagging

## 1. Tokenisation

### Principe 

* Rendre les données textuelles intelligibles à l’ordinateur 
* Découper le texte en éléments de base appelés tokens 
* Pour conserver l’association des mots on utilise les n-grams 

### Tokenisation simple

* Elément de base : un mot 
* Exemple : Ceci est un exemple. => `[ "ceci", "est", "un", "exemple", "."]` 

### N-grams

* Elément de base : N mots consécutifs 
* Exemple de 2-grams   
   Ceci est un exemple. => `[ "ceci est", "est un", "un exemple", "exemple."]` 
* Exemple de 3-grams   
   Ceci est un exemple. => `[ "ceci est un", "est un exemple", "un  exemple."]` 
   
   
## 2. Nettoyage des données

### Epuration de texte


* En général plusieurs étapes pour épurer un texte : 

   * Supprimer les mots vides. Ces mots n'ont pas de valeur ajoutée à l’analyse  
        * Exemples : la, le, les, au, aux, ce, ces, dans, … 
        * Limites : difficile sur certains cas par exemple été (la saison, plutôt signifiant) et été le participe passé du       verbe être (plutôt non signifiant) 
     
   * Retirer la ponctuation (punctuation filter) 
   * Eliminer les termes d’élision (Elision filter)
   * Mettre le texte en minuscule    
   * ...

**Note :** Ces étapes sont à adapter selon les cas par exemple :     

   * Ne pas mettre le texte texte en minuscule si les majuscules sont pertinentes  
   * Tenir compte de la langue pour la ponctuation   
   * … 
 
 ### Filtres phonétiques

* Les filtres phonétiques sont des algorithmes permettant de transcoder des mots vers des éléments de langage oraux pour limiter l’impact des fautes d’orthographe 

### Stemming

  * Le stemming consiste à réduire un mot dans sa forme « racine »
  * L'objectif est de représenter les variantes d’un mot par un seul mot
  * Exemple : `les mots petit, petits, petite, petites, petitesse, petitesses doivent être donner le même mot après application du stemming`

### Lemmatisation
   
   * La lemmatisation consiste à regrouper les tokens dans des lemmes
   * Les accords en nombre, genre du mot Les conjugaisons du mot si c’est un verbe 
   * …. 
   
   * Exemples 
      * Le lemme beau couvre les mots beaux, belle, belles … 
      * Le lemme être couvre les mots suis, es, est, étais … 

### Synonymisation

  * On regroupe les lemmes par synonyme 
  * On a pour cela besoin d’un bon dictionnaire des synonymes 

  * Exemples 
    * `ville, commune, municipalité`
    * `télévision, télé, tv` 
 
### L’étiquetage morpho-syntaxique ou le Part of Speech (POS) tagging

* Chaque mot du texte se voit attribuer un tag correspondant à sa fonction grammaticale  
 * Nom, verbe, adverbe, préposition, … 
* On enrichit ainsi la compréhension sémantique 
 * Exemple :       
    Le big-data est une révolution :    
    `Le (DET), big-data (NOM), est (VER), une (DET), révolution (NOM)`

## B. Représentation vectorielle des documents

* Transformer le corpus de texte en matrice de taille `NxD` avec : 
 * `N` est le nombre de documents dans le corpus, chaque ligne représente un document 
 * `D` est le nombre de mots du dictionnaire obtenu après préprocessing


* En général `D` et `N` sont grands et la matrice est creuse ou sparse (pleine de 0)  


* Il existe plusieurs méthodes pour créer cette matrice :
  *  Comptage des mots : compter le nombre de fois qu'apparaît dans chaque document un mot du dictionnaire
  * TF-IDF : permet de diminuer l'importance des mots très fréquents ayant une valeur ajoutée limitée 
  * Word embedding : fournit une représentation vectorielle d'un mot


## C. Analyse sémantique latente (Latent semantic analysis, LSA)

* Certaines représentations vectorielles de document ne tiennent pas compte des relations en entre les mots (exemple : nombre d'occurrences des mots, ...)


* La LSA transforme la matrice des occurrences en une « relation » entre les termes et des « concepts », et une relation entre ces concepts et les documents. On peut donc relier des documents entre eux


* Il existe plusieurs techniques pour effectuer une analyse sémantique sur ces types matrices :
 * Réduction du rang de la matrice via une décomposition en valeurs singulières (SVD).
     * Limite : fournit des valeurs négatives difficilement interprétables dans certains contextes
 * Approximation de la matrice par une factorisation matricielle non négative (NMF).
     * Limite : fournit des valeurs positives mais la décomposition n'est pas unique (peut converger vers une solution locale)
  * ...

## D. Topic modeling

* Topic modeling : processus d’extraction des différents thèmes (topics) d’un corpus.


* Le topic modeling peut être vu comme une technique de réduction de dimension :
   * Un document est représenté par un vecteur dans l'espace des thèmes du corpus (et non par rapport aux mots du vocabulaire)


* Il existe plusieurs techniques pour effectuer une analyse sémantique sur ces types matrices :

 * Calcul de la matrice de thèmes avec :
     * La SVD (Décomposition en Valeurs Singulières)
        * Limite : fournit des valeurs négatives difficilement interprétables dans certains contextes
     * La factorisation matricielle non négative (NMF).
       * Limite : les thèmes ne sont pas orthogonaux
 * LDA : modèle probabiliste génératif 
   * modéliser le processus de génération des paires documents-termes
   
 * ...
 
## E. Quelques cas d'usage

Les applications de l'analyse sont très nombreuses :

* Recherche d’information : identifier, dans un corpus, les documents pertinents relatifs à une requête
* Analyse du sentiment
* Name Entity Recognition : trouver et classifier les noms dans un texte en différentes catégories
* Classification automatiquement des documents
* Résumé du contenu d’un document 
* ...
