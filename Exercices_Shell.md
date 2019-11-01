EXERCICES
=========


### EXERCICE 1

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
   
   
### Exercice 2
On suppose que l'on se trouve dans un répertoire `TEST`, que ce dernier est vide et que l'on exécute les sept commandes suivantes :
```console
mkdir a b c d
touch a/t.txt d/foo.txt
cd c
mkdir ../b/e f g
cd ..
cp */*.txt c/g
rm -rf d
```
Dessiner l'arborescence finale des fichiers et répertoires (on uilisera `TEST`comme racine de l'arborescence)

### Exercice 3
1.  Créez, dans votre répertoire personnel, les répertoires `NSI` et `NSI/TP_SHELL`.
2.  Modifiez les permissions de telle sorte que :
	+ Le répertoire personnel possède tous les droits pour l'utilisateur et uniquement le droit d'exécution pour le groupe 
	et les autres.
	+ Les répertoires `NSI` et `NSI/TP_SHELL` possèdent tous les droits pour l'utilisateur et les droits de lecture
	et d'exécution pour le groupe et les autre (une commande par répertoire).
3. Créer un fichier `lisible.txt` dans le répertoire `NSI/TP_SHELL` . Il devra posséder les droits de lecture/écriture pour l'utilisateur et uniquement les droits de lecture pour le groupe et les autres.
4. Créer un fichier `secret.txt` dans le répertoire `NSI/TP_SHELL` . Il devra posséder les droits de lecture/écriture pour l'utilisateur et aucun droit pour le groupe et pour les autres.
5. Demander à votre voisin de tester ses droits en 
	+ essayant de lire le contenu du fichier `secret.txt`
	+ essayant de lire puis de modifier le contenu du fichier `lisible.txt`.
6. Éditez un fichier nommé `salut` avec le contenu suivant :
   ```
   echo Hello World
   ```
   Tentez de l'exécuter en tapant `./salut`. Modifiez les droits de manière à ce que vous puissiez l'exécuter
   puis vérifiez que vous pouvez l'exécuter.


   

