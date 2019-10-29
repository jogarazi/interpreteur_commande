Interface système ou Shell
=====================================================================

L'interface système (_shell_ en anglais) est un programme permettant à l'utilisateur d'interagir avec le système
d'exploitation. C'est une forme simple d'interface utilisateur.
_Shell_ (pour coquille en anglais) est le terme anglais pour désigner l'interface avec le système d'exploitation (OS, _Operating System_).
Les OS basés sur Unix disposent de deux types d'interface avec le système :
- une *interface graphique* (GUI pour _Graphical User Interface_)
- et des *interfaces en ligne de commande* (CLI pour _Command Line Interface_)

Utilisateur
-----------

Un **utilisateur**

* est identifié par son nom d'utilisateur, _nom de login_, par exemple
  `phm` ou `duchmol`. L'accès à son compte est protégé par un _mot de
  passe_, c'est un élément de sécurité, mais aussi de responsabilité (les
  actions réalisées sous ce compte sont réputées réalisées par la
  personne auquel il appartient)
* appartient à un _groupe_, par exemple `enseign`, ou `diueil`
* possède un _répertoire personnel_, répertoire de login, son
  "chez-lui", espace dédié du système de fichiers
* a des droits limités, certaines commandes ou l'accès à certains
  fichiers lui sont par exemple interdits 

Un utilisateur s'identifie auprès du système par une procédure de
_login_ après quoi il se retrouve dans un environnement graphique ou
un interpréteur de commandes.

Interpréteur de commandes ou shell
----------------------------------

L'**interpréteur de commandes** ou **shell** permet à l'utilisateur
de demander l'exécution de _commandes_. Ces commandes sont

* des commandes du système, ou
* des programmes de l'utilisateur.

L'interpréteur de commande 

* réalise diverses substitutions (de noms de variables par leur
valeur, de motifs par des noms de fichiers),
* permet de combiner plusieurs commandes, 
* permet aussi le contrôle des processus (les programmes en cours d'exécution),
* et autres...

En mode interactif, l'interpréteur de commandes, propose une invite,
un prompt, à l'utilisateur. Par exemple sous la forme du simple caractère
`$` ou `%`, ou sous la forme d'une chaîne de caractères pouvant
mentionner le nom d'utilisateur, le nom de la machine, l'heure, le
répertoire de travail, etc. \
Par exemple pour 

```console
duchmol@a12p24:~$
```
