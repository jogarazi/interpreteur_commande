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
alice@a12p24:~$ ls
alice@a12p24:~$ ls -a
alice@a12p24:~$ ls -a -l
alice@a12p24:~$ ls -la
```

Les arguments désignent les entités, par exemple les fichiers ou utilisateurs, qui
seront traités par la commande. On demandera ainsi de lister le
contenu du répertoire de nom `etc` par :

```console
alice@a12p24:~$ ls -l etc
```

Les options et arguments forment ce que l'on appelle parfois les
_paramètres_ de la commande. 

Manuel en ligne
---------------

Les commandes sont documentées dans le **manuel en ligne** auquel la commande
`man` permet d'accéder : 

```console
alice@a12p24:~$ man ls 
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
├── bin                 
├── etc			
├── home
│   └── alice
	   ├── Documents
	   │      ├── cours.odt
           │      └── diapos.pdf
	   │
	   ├── Photos
	         ├── img_001.jpg
                 └── img_002.jpg

```

L'organisation globale du système de fichier suit un standard,
[FHS, _Filesystem Hierarchy Standard_](https://fr.wikipedia.org/wiki/Filesystem_Hierarchy_Standard).

Par exemple, le répertoire `/bin` contient les commandes de base alors
que le répertoire `/etc` contient les fichiers de configuration du
système, et le répertoire `/home` les répertoires des utilisateurs. 

Ici la racine `/` contient les répertoires `bin`, `etc`, `home`, `tmp` et possiblement d'autres non affichés. Le répertoire `Documents`est un _sous-repertoire_ du répertoire `alice`, ce dernier se situant lui-même dans le sous-repertoire `home` de la racine.

Répertoire de travail
---------------------

Toute commande ou programme s'exécute dans un répertoire donné, dit le
_répertoire courant_ ou _répertoire de travail_ que l'on peut voir
comme celui dans lequel on est "positionné". \
Lorsque l'on se connecte au système, on est placé dans le répertoire
personnel, par exemple `/home/alice`. \
Des commandes du système permettent de changer de répertoire courant,
de se déplacer dans la hiérarchie du système de fichiers :

La commande `pwd` affiche le répertoire de travail :

```console
alice@a12p24:~$ pwd
/home/alice
```

La commande `cd` permet de changer de répertoire de travail :

```console 
alice@a12p24:~$ pwd
/home/alice
alice@a12p24:~$ cd Documents 
alice@a12p24:~/Documents$ pwd
/home/alice/Documents
```
Elle permet également de revenir directement au répertoire personnel de l'utilisateur lorsqu'on l'utilise sans paramètre :

```console 
alice@a12p24:~/Documents$ cd
alice@a12p24:~$ pwd
/home/alice 
```

La commande `mkdir` permet de créer un nouveau répertoire :

```console
alice@a12p24:~$ ls
Documents Photos
alice@a12p24:~$ mkdir test
alice@a12p24:~$ ls
Documents Photos test
```

La commande `rmdir` permet de supprimer un répertoire, il doit être
vide :

```console
alice@a12p24:~$ rmdir test
alice@a12p24:~$ ls 
Documents Photos
```




Chemin d'accès à un fichier
---------------------------
Les chaines de caractères affichées par les commandes ci-dessus sont des _chemins_.
Le **chemin d'accès à un fichier** permet de désigner un fichier au
sein de la hiérarchie. Il s'agit 

* d'une suite des noms des répertoires intermédiaires
* séparés par le caractère `/`
* de la racine vers la feuille

Des exemples sont :

```
/home/alice/Photos/img_002.jpg
```

ou

```
Photos/img_002.jpg
```

On distingue donc les

* chemins _absolus_
  - qui commencent par `/`
  - donnent l'ensemble du chemin depuis la racine du système de
    fichiers 
* chemins _relatifs_
  - donnent le chemin depuis le répertoire de travail

Comme on peut le voir dans les test précédents, l'interpréteur de commande permet de désigner le répertoire personnel
à l'aide du caractère `~`. On écrit par exemple 

```
~/Documents/diapos.pdf
```

pour désigner le fichier `diapos.pdf` du répertoire `Documents`.


Entrées `.`et `..`
------------------

Chaque répertoire comporte deux entrées de noms `.`et `..` qui
correspondent respectivement

* au répertoire lui même, 
* au répertoire parent.

En supposant que le répertoire courant soit `/home/alice/documents`,
on pourra écrire `../Photos` pour désigner le répertoire `/home/alice/Photos`

```console
alice@a12p24:~$ cd
alice@a12p24:~$ cd Documents
alice@a12p24:~/Documents$ cd ../Photos
alice@a12p24:~/Photos$ pwd
/home/alice/Photos
```



Permission et propriété des fichiers
------------------------------------

Le système Linux est multiutilisateur. Chaque personne utilisant une machine possède un _compte utilisateur_ sur le système et peut partager des fichiers avec d'autres utilisateurs de la machine. Comme nous l'avons vu ci-dessus, le système Linux propose en effet la notion de _groupe d'utilisateurs_. Un utilisateur doit obligatoirement être membre d'un groupe au moins.
Pour gérer cela, le système d'exploitation associe à chaque fichier l'UID de son propriétaire et le GID de son groupe propriétaire.  Le système permet aussi de définir des _permissions_ pour le propriétaire, le groupe propriétaire et les autres utilisateurs. L'option `-l`de la commande `ls` permet de faire un affichage détaillé des fichiers :

```console
alice@a12p24:~$ ls -l Photos
total 2672
-rw-r--r-- 1 alice nsi 1431099 oct. 31 7:55 img_001.jpg
-rw-r--r-- 1 alice nsi 1300458 oct. 31 7:56 img_002.jpg
```
Le resultat de la comande ci-dessus indique en premier lieu que la taille occupée par 
les fichiers fait 2672 blocs de 1024 octets.
Ensuite, pourchaque fichier , sont donnés les _permissions_, un nombre (correspondant au nombre de "liens durs" vers le fichier. Nous n'en parlerons pas dans ce cours), le nom du propriétaire, le nom du groupe propriétaire, la taille en octet, la date et l'heure de la dernière modification du fichier et enfin le nom du fichier.

### Lecture des permissions :
- le premier caractère sera `d` si la ligne concerne un répertoire et `-`sinon
- les neufs caractères suivants sont à lire par groupe de 3. Dans chaque groupe le premier caractère représente les droits en lecture (`r`pour _read_), le second les droits en écriture (`w` pour _write_) et le troisième ceux en exécution (`x`pour execute). Si une lettre est affichée la permission est accordée. Si un `-`est affiché, la permission est refusée.
- le premier groupe de trois caractères représente les permissions pour le propriétaire, le second pour le groupe propriétaire et le troisième pour tous les autres.

Dans l'exemple ci-dessus, `img.001.jpg` est un fichier (premier caractère `-`) appartenant à `alice` qui peut le lire, le modifier mais pas l'exécuter (`rw-`, l'exécution dans le cas d'un fichier image n'aurait aucun sens). Le fichier appartient également au groupe `nsi`
dont tous les membres peuvent le lire mais ni le modifier ni l'exécuter (`r--`). Enfin tous les autres utilisateurs peuvent lire le fichier mais ni le modifier ni l'exécuter (`r--`).


### Modifications des permissions

La commande `chmod` permet de modifier les permissions sur le fichier, avec la syntaxe :

```console
alice@a12p24:~$ chmod c_1m_1p_1,...,c_nm_np_n chemin
```
où 
- les `c_i` sont des cibles qui peuvent valoir `u` (pour le propriétaire), `g` (pour le groupe), `o` (pour les autres) et `a` pour tous (c'est à dire les trois catégories).
- les `m_i` sont des modifications (`+`pour dire ajouter, `-`pour dire retirer)
- les `p_i` sont des symboles de permissions (`r`, `w` ou `x`).

Par exemple la commande ci-dessous rajoute les droits en écriture à toutes les personnes du groupe et supprime les droits en lecture des autres.

```console
alice@a12p24:~$ chmod g+w,o-r Photos/img_001.jpg
alice@a12p24:~$ ls -l Photos
total 2672
-rw-rw---- 1 alice nsi 1431099 oct. 31 7:55 img_001.jpg
-rw-r--r-- 1 alice nsi 1300458 oct. 31 7:56 img_002.jpg
```
Pour illustrer les droits en exécution, on peut faire le test suivant :

```console
alice@a12p24:~$ ls -l /bin/ls
-rwxr-xr-x root root 88248 janv. 14 2019 /bin/mkdir
```

On demande ici les informations détaillées sur un fichier `mkdir`se situant dans le répertoire `bin`. Ce fichier correspond justement à l'exécutable de la commande `mkdir` que nous avons exécuter précédemment. On peut voir que ce fichier appartient à `root` (et à son groupe), c'est à dire que c'est un fichier système. Seul le super-utilisateur peut modifier ce fichier (ce qui est une opération risquée mais qui peut se produire lorsque le système est mis à jour) mais tous les autres utilisateurs pourront le lire et l'exécuter. Ainsi, toute personne peut exécuter la commande `mkdir`pour créer des répertoires.

En ce qui concerne les **répertoires**, les trois de types de permissions existent mais ont un sens propre :
- le droit en lecture sur un répertoire signifie que son _contenu_ peut être listé
- le droit en écriture signifie que l'on peut modifier des _entrées_ du répertoire c'est à dire créer des fichiers, les supprimer ou les renommer. En particulier, il n'est pas nécessaire d'avoir les droits en écriture sur un fichier pour le supprimer mais il faut avoir les droits en écriture de son `répertoire parent`.
- le droit en exécution pour un répertoire signifie que l'on a le droit d'en faire le répertoire courant et d'afficher les informations détaillées sur les entrées du répertoire.

Supposons dans l'exemple suivant que l'on dispose d'un autre utilisateur, dont l'identifiant est `bob` et le groupe principal est `terminale` (c'est à dire n'appartenant pas au groupe d'Alice).

```console
alice@a12p24:~$ chmod o-r home/alice
alice@a12p24:~$ ls -l -d /home/alice
drwxr-x--x 1 alice nsi 4096 31 oct 7:55 /home/alice
```
Ici l'option `-d` de la commande `ls` permet d'afficher les informations du répertoire `/home/alice` plutôt que de lister son contenu (comme on a pu le voir grâce à la commande `man` précédemment).
Si `bob`ouvre une session à son tour, il ne peut pas voir le contenu du répertoire personnel d'Alice :

```console
bob@a12p24:~$ cd home/alice
bob@a12p24:~$ ls -l 
ls: impossible d'ouvrir le répertoire '.' : Permission non accordée
```
Si Alice remet les droits en lecture et retire les droits en exécution, 

```console
alice@a12p24:~$ chmod o+r,o-x home/alice
alice@a12p24:~$ ls -l -d /home/alice
drwxr-xr-- 1 alice nsi 4096 31 oct 7:55 /home/alice
```

L'utilisateur `bob`pourra alors lire les entrées, mais pas les informations associées et ne pourra pas pénétrer dans le répertoire.

```console
bob@a12p24:~$ ls -l home/alice
ls: impossible d'accéder à '/home/alice/Photos' : Permission non accordée
ls: impossible d'accéder à '/home/alice/Documents' : Permission non accordée
total 0
d????????? ? ? ? ? 				? Documents
d????????? ? ? ? ?				? Photos
bob@a12p24:~$ cd /home/alice
bash: cd: /home/alice/: Permission non accordée
```



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
* le motif `*z*` par rien (et le shell avertira d'une erreur) 

D'autres méta-caractères sont définis :

* `[liste]` correspond à n'importe quel des caractères de _liste_
* `[^liste]` correspond à n'importe quel des caractères sauf ceux de _liste_
* `[lower-upper]` correspond à tout caractère compris entre _lower_ et _upper_

Par exemple : 

```console
alice@a12p24:~$ ls /home/alice/*/img?*[23].jpg
/home/alice/Photos/img_002.jpg
alice@a12p24:~$ ls /home/alice/Photos/photos*
ls: impossible d'accéder à '/home/alice/Photos/photos*' : Aucun fichier ou dossier de ce type

```

Pour complèter ce cours, vous trouverez une référence
des principales commandes de manipulation du système de fichiers à
[fr.wikipedia.org/wiki/Commandes_Unix#Fichiers_et_répertoires](https://fr.wikipedia.org/wiki/Commandes_Unix#Fichiers_et_r%C3%A9pertoires). 

Voyez également la carte de référence Unix de Moïse Valvassori 

* [unix-refcard.pdf sur www.ai.univ-paris8.fr](http://www.ai.univ-paris8.fr/~djedi/poo/unix-refcard.pdf)


EXERCICES
---------
## EXERCICE 1

1. Utilisez la commande `ls` pour lister l'ensemble des fichiers présents dans le 
   répertoire courant.
1. Nous allons maintenant créer un nouveau répertoire : utilisez la commande `mkdir` 
   suivie du nom du répertoire. Ici `mkdir TP_shell`. Observez le résultat par une nouvelle exécution de `ls`. 
1. Déplaçons nous dans le répertoire TP_shell nouvellement créé : `cd TP_shell`. Constatez que l'invite de l'interpréteur a été modifiée, indiquant que nous sommes maintenant dans le répertoire `TP_shell`.
1. Utilisez la commande `pwd` pour afficher le répertoire courant.
1. Pour les besoins du TP, 
   * créons un nouveau répertoire : `mkdir bob`
   * plaçons nous dans ce répertoire : `cd bob`
   * affichons le répertoire courant : `pwd`
1. Nous allons créer un fichier dans le répertoire `bob` :
   * La commande `touch test` crée un fichier (vide) appelé `test`,
   * Vérifions à l'aide de la commande `ls` que le fichier a bien été créé.
1. Remontons dans l'arborescence : 
   * `cd ..` 
   * Vérifions que le répertoire courant a bien été modifié : `pwd`
   * Créons un deuxième répertoire : `mkdir eve`
1. Pour *copier un fichier* :
   * on utilise la commande `cp` : `cp bob/test eve/`
   * Cette commande a pour effet de copier le fichier `test` dans le 
	 répertoire `eve/`
   * Afficher le contenu du répertoire `eve`
1. Nous allons maintenant tenter de supprimer le répertoire `bob` : 
   * `rmdir bob` vous constatez que la commande produit une erreur puisque le répertoire n'est pas vide.
   * Il est possible de supprimer un répertoire non vide, mais pour 
	 l'instant allons effacer le fichier `test` qui n'est de toute façon pas d'une grande utilité : `cd bob` puis `rm test` (remove).
1. Tentons à nouveau la suppression du répertoire : 
    * `cd ..` 
    * `rmdir bob`
	
	Vous constatez que la commande ne signale plus d'erreur et que le 
	répertoire a été supprimé.
1. Nous pouvons également déplacer des fichiers : 
    * `mv eve/test .`
   
   Cette commande déplace (move) le fichier `test` de `eve` dans 
   le répertoire courant `./` (ici `TP_shell`).
1. La même commande `mv` permet aussi de renommer un fichier. Essayez
   `mv test essai`. Observez. 
1. Le répertoire `eve` ne contient plus rien : 
   * `ls eve/` 
   * Nous pouvons le supprimer : `rmdir eve`
1. Saisissons les commandes suivantes :
   * `cp essai Essai`
   * `ls`
   
   Observez que le répertoire contient maintenant deux fichiers *différents*
   dont les noms sont `essai` et `Essai` : Le système de fichier est donc
   *sensible à la casse*.
1. Saisissons :
   * `cp essai .essai`
   * `ls`
   
   Observez que le contenu du répertoire ne semble pas avoir été modifié. Pourtant 
   le fichier `.arthur` a bien été créé :
   * `ls .arthur`
   
   Il s'agit d'un *fichier caché*. 
   La convention adoptée et que tous les fichiers dont le nom commence 
   par un point `.` sont traités comme des fichiers cachés.
1. Pour visualiser *tous* les fichiers d'un répertoire (y compris les cachés) :
   * `ls -a`
   * ou `ls -al` 
   
   Observez la différence entre les deux commandes. 
   Testez `ls` avec l'option `-l` seule. En déduire l'effet de l'option `-l`. 
1. Observons que notre répertoire contient une entrée nommée `.` qui représente 
   le répertoire courant et une entrée nommée `..` qui correspond au répertoire
   supérieur. On retrouve ces deux entrées dans tous les répertoires.
1. Nettoyons maintenant notre répertoire :
   * `rm essai Essai .essai` (la commande `rm` accepte plusieurs arguments)
   * `cd ..`
   * `rmdir TP_shell`



