# Git


## Intro

## Sommaire

  1. Pré-requis 🏫
  2. Notions théoriques et vocabulaire 🏫
  3. Les commandes de base 🏫
  4. Les étapes de la création d'un projet git 🏫

## 1. Pré-requis

  * pour les windowsiens : **git bash**, à télécharger sur le site officiel [git scm](https://git-scm.org)
  * pour les linuxiens : **git** depuis les dépôts officiels de votre distrib'
  * pour les macqueux : bah git est préinstallé de base il me semble :)
  * pour tous : [VS Code](https://code.visualstudio.com)
  * une fois VS Code installé, ajoutez les extensions "Draw.io integration" et "Markdown Preview Enhanced"
  * un compte sur [Github](https://github.com) ou [Gitlab](https://gitlab.com) (gratuit mais nécessite une carte bancaire pour gitlab)

## 2. Notions théoriques et vocabulaire

  * **remote** : dépôt de référence
  * **clone** : action de récupérer un nouveau projet complet en local depuis le dépôt de référence
  * **commit** : point de sauvegarde du code. On commit dès qu'on a quelque chose qui marche, le plus souvent possible
  * **branche** : version alternative du projet. La branche principale s'appelle *main* depuis 2020 sur la plupart des outils utilisant git.
  * **push** : action d'envoyer ses modifications locales vers le dépôt de référence
  * **pull** : action de récupérer les dernières mises à jour du dépôt local vers son dépôt local
  * **checkout** : basculer de branche / revenir à un commit précédent
  * **merge** : fusionner les modifications d'une branche alternative vers la branche courante
  * **merge request** ou **MR** : action sur un site type Github ou Gitlab, demandant de déclencher un merge vers une branche spécifique (souvent la branche principale)

## 3. Commandes de base

  * configurer son git local (à faire une fois) : `git config --global user.name "Votre nom ici"` et `git config --global user.email "votre mail ici"`
  * Cloner un dépôt : `git clone url-du-depot` Par défaut, le git clone va créer un sous-dossier portant le nom du projet, et le cloner dedans.
  * Faire un commit : `git add .` (notez le point final) suivi de `git commit -m "Commentaire obligatoire ici"` Si vous oubliez le commentaire, git va ouvrir un éditeur (nano ou vi) pour vous forcer à en ajouter un.
  * Vérifier le statut d'un dépôt local : `git status`
  * Afficher l'historique des commits de la branche : `git log` (appuyez sur 'q' pour quitter)
  * Afficher les branches locales : `git branch`
  * Afficher les branches locales et les branches distantes : `git branche -a`
  * Créer une nouvelle branche : `git branch nom-de-la-nouvelle-branche`
  * Créer une nouvelle branche et basculer dessus immédiatement : `git checkout -b nom-de-la-nouvelle-branche`
  * Basculer vers une branche spécifique, par exemple main : `git checkout main`
  * Récupérer les modifications du dépôt de référence : `git fetch`
  * Récupérer et appliquer les modifications du dépôt de référence à la branche courante : `git pull`
  * Envoyer ses modifications locales au dépôt de référence : `git push`

## 4. Les étapes de la création d'un projet git 🏫

  * Se connecter sur GitHub
  * Créer un nouveau dépôt (repository)
    * si vous le mettez en public, tout le monde pourra voir votre code (à privilégier pour les exercices)
    * si vous le mettez en privé, il faudra inviter les membres pour qu'ils puissent voir le code (à faire pour les rendus)
    * **cochez impérativement la case "Add a README file"**
  * Si vous avez besoin d'ajouter quelqu'un au dépôt (formateur ou binôme/groupe) : cliquez sur "Settings", puis "Collaborators", puis "Add people" et rentrez l'adresse email des personnes à inviter
  * cliquez ensuite sur "<> Code" en haut à gauche
  * cliquez sur l'onglet "Clone with HTTPS" (vous verrez la gestion des clés SSH - beaucoup plus sécurisées - lors du module Linux)
  * copiez l'url de clone
  * Si vous utilisez VS Code : 
    * Dans VSCode, ouvrez la palette avec Ctrl-P
    * dans la palette, tapez "> Git Clone"
    * Collez l'URL du dépôt
    * Renseignez vos identifiants
    * Sélectionnez le dossier dans lequel vous souhaitez cloner votre dépôt. Je vous conseille TRÈS fortement de ne **PAS** mettre vos projets sur le Bureau (on ne met RIEN sur le bureau, merci).
    * Validez, le projet est cloné et s'ouvre dans VS Code
  * Avec git bash : 
    * se positionner à l'endroit où vous voulez cloner le dépôt avec `cd chemin\vers\le\dossier`
    * clonez avec `git clone ` suivi de l'url de clone, puis validez
    * renseignez vos identifiants lorsqu'ils sont demandés
    * dans l'explorateur de fichiers, vous pouvez faire un clic droit sur le dossier, puis "Ouvrir avec Code" pour ouvrir le projet avec VS Code, ou travailler normalement