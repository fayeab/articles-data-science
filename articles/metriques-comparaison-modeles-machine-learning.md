# Quelques métriques pour la comparaison de modèles

Nécessité d’évaluer les modèles de prédiction :
* Évaluer les performances d’un modèle de prédiction est primordial. Pour savoir si le modèle est globalement significatif.
* Mon modèle traduit-il vraiment une causalité ? Pour se donner une idée des performances en déploiement.
* Quelle sera la fiabilité (les coûts associés) lorsque j’utiliserai mon modèle ? Pour comparer plusieurs modèles candidats.
* Lequel parmi plusieurs modèles sera le plus performant compte tenu de mes objectifs ?

## 1. Classification

####  Courbe de ROC

Supposons que nous avons un classifieur qui classe des observations en un ensemble de classes. De plus, il donne cette réponse accompagnée d’un score de pertinence. Deux cas sont possibles : soit la réponse est bonne (1), soit la réponse est fausse (0). Pour chaque observation, on associe un couple (r,x) où r est égal à 0 ou 1. x est le score de pertinence. On cherche à déterminer à partir de quel seuil de pertinence, la réponse du classifieuur est fiable. En faisant varier x, on obtient une courbe (source : wikipedia).

####  Choix du seuil optimal à l’aide de la courbe ROC

Le seuil correspondant
* au point le plus proche de l’idéal (1, 1)
* au point le plus loin de la diagonale 

#### L’AUC ou surface sous la courbe ROC (Area Under Curve)

* Plus l’AUC est grand, meilleur est le test.
* Fournit un ordre partiel sur les tests
* Problème si les courbes ROC se croisent
* Courbe ROC et surface sont des mesures intrinsèques de séparabilité, invariantes pour toute transformation monotone croissante de la mesure S

#### Le recall (rappel ou sensibilité) et la précision

$T_p$ (Vrais positifs): représente le nombre d'individus déclarés positifs alors qu'ils le sont

$F_p$ (Faux positifs) :  représente le nombre d'individus déclarés positifs à tort

$T_n$ (Vrais negatifs): représente le nombre déclarés négatifs alors qu'ils le  sont

$T_n$ (Faux negatifs) : représente le nombre déclarés négatifs à tort

$$ \text{Précision} = \frac{ T_p}{T_p + F_p}$$

$$ \text{Recall} = \frac{ T_p}{T_p + F_n}$$

$$ \text{Spécificité} = \frac{ T_n}{F_p + T_n} = 1 - \frac{ F_p}{F_n + T_n} $$

$$ \text{F1-Score} = \frac{ \text{Précision} \times \text{Recall}}{2\times(\text{Précision} + \text{Recall})}$$

**Exemple**
* Sensibilité : proportion de vrais positifs parmi les personnes à dépister
* Spécificité : proportion de vrais négatifs chez les non-malades:
* **Remarque**
    * Facile d’avoir une bonne sensibilité: déclarer tout le monde positif… mais peu spécifique
    * Un bon test doit être sensible et spécifique



## 2. Régression

Voici quelques indicateurs permettant de mesurer la qualité d'une prévision pour une régression. 

**SCR ou Sum of Squared Errors)**

La somme des carrés des résidus (SCR ou Sum of Squared Errors). Comme on mesure des carrés, on majore l’importance des grosses erreurs.
$$SCR = \sum_{k=1}^{n} (Y_k - \hat{Y}_k)^2$$

**MSE pour Mean Square Error ou MCE pour moyenne des carrés des erreurs**

Le carré moyen des erreurs ou erreur quadratique moyenne (MSE pour Mean Square Error ou MCE pour moyenne des carrés des erreurs) : c’est la moyenne arithmétique des carrés des écarts entre les prévisions et les observations.
C’est la valeur à minimiser dans le cadre d’une régression simple ou multiple. La méthode est fondée sur la nullité de la moyenne des résidus. Mais la moyenne de leurs carrés n'est généralement pas nulle. Cette moyenne n'est autre que la VARIANCE RÉSIDUELLE que l'on cherche à minimiser.

La formule de calcul change selon le contexte puisque la somme des carrés est divisée par un nombre de degrés de liberté:
* Cas d’une série chronologique :
 $$MSE = \frac{SCR}{n}$$
* Cas d'une régression simple : 
$$MSE = \frac{SCR}{n – 2}$$
* Cas d'une régression multiple ($k$ = nombre de variables explicatives):
$$MSE = \frac{SCR}{n – k - 1}$$

Si l'on compare deux estimateurs sans biais, le meilleur est bien sûr celui qui présente le MSE le plus faible.

**L’erreur-type (RMSE) : racine carrée du précédent**

$$RMSE =\sqrt{ MSE}$$

L’erreur absolue moyenne (MAE pour Mean Absolute Error) : moyenne arithmétique des valeurs absolues des écarts.
$$MAE = \frac{1}{n}\sum_{k=1}^{n} \left| Y_k - \hat{Y}_k \right|$$

**Mean Absolute Percentage Error (MAPE)**

L’erreur absolue moyenne en pourcentage (Mean Absolute Percentage Error, alias MAPE) : moyenne des écarts en valeur absolue par rapport aux valeurs observées.

$$MAPE = \frac{1}{n}\sum_{k=1}^{n} \left| \frac{Y_k - \hat{Y}_k}{Y_k} \right|$$

C’est donc un pourcentage et par conséquent un indicateur pratique de comparaison. Hélas, petit inconvénient, le MAPE ne peut s’appliquer qu’à des valeurs strictement POSITIVES. Il permet donc de juger si le système de prévision des ventes est bon, mais il est inefficace pour apprécier la qualité d’estimations de résultats qui peuvent être soit des bénéfices soit des pertes (ça tombe bien, il est un peu stupide de prévoir directement un solde plutôt que ces composantes positives ou négatives).

**Coefficient de détermination et R²**

$$R^2 = 1 - \frac{SCR}{SCT}$$

Avec SCT est la somme des carrés totaux :
$$SCT = \sum_{k=1}^{n} (Y_k - \bar{Y})^2$$

Sources :   
[Ricco RAKOTOMALALA](http://eric.univ-lyon2.fr/~ricco/cours/slides/roc_curve.pdf)   
[Gilbert SAPORTA](http://cedric.cnam.fr/~saporta/Sensibilite_specificiteSTA201.pdf)   
[Jean-Yves BAUDOT](http://www.jybaudot.fr/Stats/indicecarts.html)  
[Xavier DUPRE](http://www.xavierdupre.fr/)
