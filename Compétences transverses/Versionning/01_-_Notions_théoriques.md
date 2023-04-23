# Versionning - Notions théoriques

## Sommaire

  1. Pourquoi la gestion de version ? 🏫
  2. Un peu de vocabulaire 🏫
  3. Gestion centralisée ✨
  4. Gestion décentralisée 🏫


## 1. Pourquoi la gestion de version ? 🏫

La gestion de version offre 4 avantages :

  * toujours bénéficier d'une version de production stable => on travaille sur des versions alternatives du projet, et on fusionne les fonctionnalités au fur et à mesure de leur développement dans la version de production
  * pouvoir revenir en arrière à n'importe quel moment => si une version s'avère pleine de bugs, on peut facilement revenir à la version précédente le temps de les corriger
  * pouvoir travailler à plusieurs, sans écraser par accident le travail de ses collègues
  * le dossier de travail en local reste propre : pas de copie, copiev2, copie-finale, etc


## 2. Un peu de vocabulaire 🏫

* **dépôt** : un dépôt est un répertoire spécial, contenant le code, et toutes ses versions
* **version de référence** : version du code considérée comme "valide" par tous les membres de l'équipe
* **branche** : version alternative du code, un peu comme si vous aviez un dossier "version1", "exercice2", etc
* **version de travail** : version du code actuellement active dans le logiciel de développement
* **basculement** : action de basculer d'une version active à une autre : on change "à la volée" la version de travail
* **synchronisation** : action de synchroniser la version de travail avec la version de référence du dépôt
* **commit** : point de sauvegarde dans le travail, pour pouvoir revenir en arrière
* **tag** : étiquette compréhensible par un humain, rattachée à un commit, pour pouvoir le retrouver plus facilement
* **numéro de version** : numéro rattaché à une version spécifique du code, pour pouvoir la retrouver facilement
  * numéro de version *majeure* : 3.0, 4.0, 6.0 => on change le numéro de version majeure lorsqu'on casse la rétro-compatibilité du projet. Exemple : on introduit un nouveau format de fichier que la version précédente ne pourra pas ouvrir
  * numéro de version *mineure* : 3.1, 4.2, 6.5 => on change le numéro de version mineure lorsqu'on introduit une nouvelle fonctionnalité au projet, sans casser la rétro-compatibilité. Exemple : possibilité de sauvegarder au format PDF, etc
  * numéro de *correctif* : 3.1.1, 4.2.6 => on change le numéro de correctif quand on corrige un bug ou une faille de sécurité, sans modifier le fonctionnement du logiciel

## 3. Gestion centralisée ✨

En gestion centralisée, il y a un seul dépôt central, hébergé sur un serveur auquel il faut pouvoir se connecter pour pouvoir travailler.
Impossible d'enregistrer un "point de sauvegarde", ou de basculer, sans connexion.

Exemples de logiciels de gestion centralisée de version : CVS, SVN


## 4. Gestion décentralisée 🏫

En gestion décentralisée, chaque développeur dispose de son propre dépôt local, relié à un dépôt de référence généralement hébergé sur un serveur.  
En gestion décentralisée, une connexion n'est nécessaire que pour partager son code avec le dépôt de référence. Il reste possible de travailler même isolé du réseau, puisque le dépôt local enregistre les différentes versions. Il sera ensuite possible de relancer une synchronisation avec le dépôt de référence une fois reconnecté.

Exemples de logiciels de gestion décentralisée de version : Git, Mercurial, BitBucket