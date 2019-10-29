Interface système ou Shell
=====================================================================

L'interface système (_shell_ en anglais) est un programme permettant à l'utilisateur d'interagir avec le système
d'exploitation. C'est une forme simple d'interface utilisateur.
_Shell_ (pour coquille en anglais) est le terme anglais pour désigner l'interface avec le système d'exploitation (OS, _Operating System_).
Les OS basés sur Unix disposent de deux types d'interface avec le système :
- une *interface graphique* (GUI pour _Graphical User Interface_)
- et des *interfaces en ligne de commande* (CLI pour _Command Line Interface_)

Les deux types d'interfaces offrent à peu près à l'utilisateur les mêmes fonctionnalités : navigation dans l'arborescence 
du système, créations, suppressions, éditions de répertoires et de fichiers, lancement de programmes,...)

On tachera ici de découvrir l'interpréteur de commande, quelques-unes de ses commandes de bases et la gestion des droits et permissions 
d'accès au fichier.

Utilisateurs et groupes
-----------------------

Un **utilisateur**

* est identifié par son nom d'utilisateur, _nom de login_, par exemple
  `alice`. L'accès à son compte est protégé par un _mot de
  passe_, c'est un élément de sécurité, mais aussi de responsabilité (les
  actions réalisées sous ce compte sont réputées réalisées par la
  personne auquel il appartient)
* appartient à un _groupe_, par exemple `nsi`
* possède un _répertoire personnel_, répertoire de login, son
  "chez-lui", espace dédié du système de fichiers
* a des droits limités, certaines commandes ou l'accès à certains
  fichiers lui sont par exemple interdits 

Un utilisateur s'identifie auprès du système par une procédure de
_login_ après quoi il se retrouve dans un environnement graphique ou
un interpréteur de commandes. 

Après avoir lancé l'émulateur de terminal présent sur 
votre bureau, vous devriez obtenir :

```console
alice@a12p24:~$
```




Syntaxe d'une commande
----------------------

La syntaxe des commandes saisies par l'utilisateur répond au schéma
suivant :

```
nom [option]... [argument]...
```

le premier mot est le nom de la commande, les _options_ sont de la forme `-l`,
`-a`, ou `-la`,... On écrit par exemple pour la
commande `ls` (qui liste les entrées du système de fichiers) : 

(les résultats des commandes ne sont pas affichées.)

```console
% ls
% ls -a
% ls -a -l
% ls -la
```

Les arguments désignent les entités, par exemple les fichiers ou utilisateurs, qui
seront traités par la commande. On demandera ainsi de lister le
contenu du répertoire de nom `etc` par :

```console
% ls -l etc
```

Les options et arguments forment ce que l'on appelle parfois les
_paramètres_ de la commande. 

Manuel en ligne
---------------

Les commandes sont documentées dans le **manuel en ligne** auquel la commande
`man` permet d'accéder : 

```console
% man ls 
LS(1)                                      User Commands                                      LS(1)

NAME
       ls - list directory contents
SYNOPSIS
       ls [OPTION]... [FILE]...
DESCRIPTION
       List information about the FILEs (the current directory by default).  Sort entries alphabet‐
       ically if none of -cftuvSUX nor --sort is specified.

       Mandatory arguments to long options are mandatory for short options too.

       -a, --all
              do not ignore entries starting with .
       -A, --almost-all
              do not list implied . and ..
       --author
              with -l, print the author of each file

 Manual page ls(1) line 1 (press h for help or q to quit)
``` 

Pour naviguer dans une  page du manuel, on utilise la touche
d'espacement, parfois les flèches vers le haut et vers le bas. \
On sort généralement d'une page avec la touche Q. \
On effectue une recherche dans une page de manuel avec la commande
`/motif` (motif étant par exemple le mot recherché). On passe
à l'occurrence suivante du motif en appuyant sur `n`.




Arborescence de répertoires
---------------------------
L'ordinateur stocke sur son disque dur des **fichiers**, contenant des données. Il peuvent être lus, 
modifiés, renommés, copiés ou supprimés. Ces fichiers sont organisés dans une unique **arborescence de répertoires** :

* chaque fichier est dans un répertoire
* il existe un répertoire _racine_  noté `/`
* chaque répertoire a un répertoire père unique

Voici un exemple d'extrait d'arborescence :

```
/
├── bin                 `contient les commandes de bases
├── etc			contient les fichiers de configuration système
├── home
│   └── petery
├── lib
│   ├── firmware
│   ├── modules
├── media
│   ├── cdrom
│   └── petery
├── mnt
├── opt
├── proc
├── root
├── run
├── tmp
├── usr
│   ├── bin
│   ├── lib
└── var
	├── log
	├── mail
```

L'organisation globale du système de fichier suit un standard,
[FHS, _Filesystem Hierarchy Standard_](https://fr.wikipedia.org/wiki/Filesystem_Hierarchy_Standard).

Par exemple, le répertoire `/bin` contient les commandes de base alors
que le répertoire `/etc` contient les fichiers de configuration du
système, et le répertoire `/home` les répertoires des utilisateurs. 

Répertoire de travail
---------------------

Toute commande ou programme s'exécute dans un répertoire donné, dit le
_répertoire courant_ ou _répertoire de travail_ que l'on peut voir
comme celui dans lequel on est "positionné". \
Lorsque l'on se connecte au système, on est placé dans répertoire
personnel, par exemple `/home/diueil/duchmlol`. \
Des commandes du système permettent de changer de répertoire courant,
de se déplacer dans la hiérarchie du système de fichiers.

Chemin d'accès à un fichier
---------------------------

Le **chemin d'accès à un fichier** permet de désigner un fichier au
sein de la hiérarchie. Il s'agit 

* d'une suite des noms des répertoires intermédiaires
* séparés par le caractère `/`
* de la racine vers la feuille

Des exemples sont :

```
/usr/local/bin/jupyter-notebook
```

ou

```
pj/diu-eil-lil/bloc3/seance0/shell.md
```

On distingue donc les

* chemins _absolus_
  - qui commencent par `/`
  - donnent l'ensemble du chemin depuis la racine du système de
    fichiers 
* chemins _relatifs_
  - donnent le chemin depuis le répertoire de travail

L'interpréteur de commande permet de désigner le répertoire personnel
à l'aide du caractère `~`. On écrit par exemple 

```
~/tmp/convert.py
```

pour désigner le fichier `convert.py` de mon répertoire `tmp`.


Entrées `.`et `..`
------------------

Chaque répertoire comporte deux entrées de noms `.`et `..` qui
correspondent respectivement

* au répertoire lui même, 
* au répertoire parent.

En supposant

* que le répertoire courant soit `/home/diueil/duchmol/tmp`,
* qu'il existe un répertoire ``/home/diueil/duchmol/doc`,

on pourra écrire `../doc` pour désigner ce répertoire.

Syntaxe d'un nom de fichier
---------------------------

Le **nom de fichier** correspond au nom du fichier dans le répertoire
auquel il appartient. Ce nom

* est une suite de caractères (sauf le `/`)
* de longueur limitée (255, ou 1024 caractères selon la configuration
  du système)

On évite en général l'usage du caractère espace et des lettres
accentuées.

UNIX fait une différence entre les lettres en capitales et en
minuscules. Ainsi, `toto` et `Toto` désignent deux fichiers
différents.

Le système n'impose pas de contraintes, mais on utilise des extensions
ou suffixes conventionnels. Par exemple `.c` et `.h` pour les fichiers
sources C, `.java` et `.class` pour Java, `.py` pour Python, `.html`
ou  `htm` pour des fichiers au format HTML,  `.jpeg` ou `. jpg` pour
des fichiers contenant des images au format JPEG,  `.md` ou
`.markdown`  pour des fichiers textes au format Markdown, `.tex` au
format LaTeX, etc. 

L'absence de suffixe est généralement réservée aux fichiers
exécutables et aux répertoires.

Les fichiers dont le nom commence par le caractère `.` sont considérés
comme des fichiers "cachés". Par défaut ils ne sont pas affichés quand
on liste le contenu d'un répertoire.

Méta-caractères
---------------

Le shell réalise la substitution de **méta-caractères**. Il s'agit
principalement de `*` et `?`. Un mot qui comporte ces méta-caractères
est un motif, on parle aussi d'expression régulière. Un tel motif
correspond à un ensemble de mots possibles. Ce motif sera remplacé par
le shell par l'ensemble des noms de fichiers qui correspondent,
sachant que 

* le caractère `?` correspond à un caractère quelconque
  (y compris le `.`)
* le caractère `*`correspond à une suite quelconque de caractères
  (éventuellement vide)

Ainsi, si existe les fichiers `test`, `time`, `touch`, `trace`,
`troff`, `true`, et `tsort`,

* le motif `t*` sera remplacé par l'ensemble des noms de fichiers,
* le motif `*s*` par `test`, et `tsort`,
* le motif `tr???` par les seuls `trace` et `troff`
* le motif `*z*` par rien (et el shell avertira d'une erreur) 

D'autres méta-caractères sont définis :

* `[liste]` correspond à n'importe quel des caractères de _liste_
* `[^liste]` correspond à n'importe quel des caractères sauf ceux de _liste_
* `[lower-upper]` correspond à tout caractère compris entre _lower_ et _upper_

Manipulation des répertoires
----------------------------

La commande `pwd` affiche le répertoire de travail :

```console
% pwd
/home/diueil/duchmol/tmp
```

La commande `cd` permet de changer de répertoire de travail :

```console 
% pwd
/home/diueil/duchmol
% cd tmp 
% pwd
/home/diueil/duchmol/tmp
% cd ../doc
% pwd
/home.diueil/duchmol/doc
```

La commande `mkdir` permet de créer un nouveau répertoire :

```console
% ls
doc  tmp
% mkdir foo
% ls
doc  foo  tmp
```

La commande `rmdir` permet de supprimer un répertoire, il doit être
vide :

```console
% rmdir foo
% ls 
doc  tmp
```

Caractéristiques d'un fichier
-----------------------------

Un fichier est caractérisé par :

* un propriétaire : un des utilisateurs du système,
  par exemple `duchmol`
* un groupe propriétaire, un des groupes du système, 
  par exemple `diueil`
* des dates (de création, de dernière modification, etc.)
* des droits d'accès
  - en lecture, écriture, exécution
  - pour le propriétaire, pour les membres du groupe propriétaire,
    pour les autres 
* un type : fichier, répertoire, lien, etc
* un numéro d'inœud (à suivre)
* etc.

La commande `ls` permet d'afficher certaines des caractéristiques :

```console
% ls -l /boot/vmlinuz
-rw------- 1 root root 8298232 Apr  3 10:07 /boot/vmlinuz
```
On y lit (en gras les principaux champs)

* premier champ **type** du fichuer et **droits** (voir ci-dessous)
* deuxième champ, un entier, le nombre de liens (physiques) vers le fichier
* troisième champ **propriétaire**, le nom du propriétaire du fichier 
* quatrième champ, le nom du groupe propriétaire du fichier 
* cinquième champ **taille**, la taille en octets (caractères) du
  fichier (une version plus lisible est possible avec l'option `-h` de
  la commande `ls`)
* champs suivants **date**, date de modification du fichier (mois,
  quantième, heure ou année)
* dernier champ **nom du fichier**

Type de fichier **todo** à compléter

Droits **todo** à compléter


Contenu d'un répertoire
-----------------------

La commande `ls` permet de lister les entrées d'un répertoire ou les
fichiers dont les noms sont donnés. Différentes options permettent
d'afficher certaines caractéristiques des fichiers.

Par défaut, la commande liste les entrées du répertoire courant.

Les options suivante sont couramment utilisées :

* `-l` - _long_ - format long, voir ci-dessus
* `-a` - _all_ - liste aussi les fiches "cachés", c.-à-d. dont le nom
  commence par `.`
* `-h`, _human-readable_ - affiche les tailles dans un format plus
  lisible
* `-R` - _recursively_ - liste récursivement les répertoires rencontrés
* `-1` - liste les fichiers à raison d'un par ligne (commode pour
  exploiter le résultat de la commande) 
* `-d` - _directory_ - les répertoires listés en paramètre sont
  affichés plutôt que de lister leur contenu 
* `-t` - _time_ - trie les fichiers, dernier modifié en tête
* `-F` - précise le type du fichier par un préfixe (`/`pour les
  répertoires, `*`pour les exécutables, `@` pour les liens
  symboliques, etc.)

La commande `tree` permet aussi d'afficher l'arborescence d'un
répertoire sous la forme d'un arbre.


**todo** ... liens symbolique / physique ...


Pour complèter cette brève introdcution, vous trouverez une référence
des principales commandes de manipulation du système de fichiers à
[fr.wikipedia.org/wiki/Commandes_Unix#Fichiers_et_répertoires](https://fr.wikipedia.org/wiki/Commandes_Unix#Fichiers_et_r%C3%A9pertoires). 

Voyez également la carte de référence Unix de Moïse Valvassori 

* [unix-refcard.pdf sur www.ai.univ-paris8.fr](http://www.ai.univ-paris8.fr/~djedi/poo/unix-refcard.pdf)
* [copie locale](doc/unix-refcard.pdf)


