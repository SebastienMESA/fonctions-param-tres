# Les fonctions à paramètres 

Essayons de comprendre à quoi servent ces foutus **paramètres**.

Sortons un peu du code pour faire un parallèle avec nos chers mathématiques (lol)

- Imaginons une fonction mathématiques très simple :

```
f(x) = x + 6;
```
dans cette exemple, la fonction ajoute "6" à "x".

- Lorsqu'on aura besoin de cette fonction, on pourra renseigner la valeur de x. Admettons par exemple que x = 5 :
```
f(5) = 5 + 6;
```

Génial !

Et bien en code c'est pareil !

- Imaginons cette fois-ci une fonction Javascript très simple :

```Javascript
function hello (parametre) {
    console.log(parametre)
}
```
Dans cette exemple, on a construit une fonction qui, lorsqu'elle sera appelée, affichera dans la console ce qu'on a renseigné en **paramètre**.

- Si on souhaite appeler notre fonction avec le **parametre** "Hello world !" :

```Javascript
function hello (parametre) {
    console.log(parametre)
}
hello("Hello world !");
// **Je suis la console** => Hello world !

// Ce que notre fonction fait réellement :
console.log("Hello world !") // la fonction remplace le mot parametre par notre "Hello world !"  et elle le fait à tous les endroits dans notre fonction où on a mis le mot parametre !

```

- Dans notre exemple de ce matin, on avait une fonction :

```Javascript
function getRandomNumber(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
```
Nous avons indiqué des **paramètres** (min et max) à cette fonction. 

Lorsqu'on construit notre fonction, on ne lui demande pas de faire quoique ce soit, on lui explique juste comment elle va devoir fonctionner. Il faudra l'appeler pour qu'elle fasse ce qu'on lui demande

- Dans notre cas ici, notre fonction getRandomNumber **_ne peut pas fonctionner sans paramètre_** exemple :

```Javascript
function getRandomNumber() {
    return Math.floor(Math.random() * (??? - ??? + 1)) + ???;
}
```
↑ On peut voir que ça n'a pas de sens de lui demander de nous retourner un nombre sans lui donner de paramètres  ↑



**⚠⚠⚠** Ces paramètres n'ont rien à voir avec nos clés/valeurs game.min et game.max de notre objet game **⚠⚠⚠**.

- notre **objet** de ce matin : 

```Javascript
const game = {
    min = 0,
    max = 500,
}
```

Maintenant, notre objectif est de faire fonctionner notre fonction getRandomNumber en lui donnant comme **paramètre** les **valeurs** contenus dans game.min et game.max

- On peut faire de cette manière :

```Javascript
// Je redéclare la fonction et l'objet juste pour plus de clarté, pour tout avoir en visu.
const game = {
    min = 0,
    max = 500,
}

function getRandomNumber(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

getRandomNumber(game.min, game.max);
```

Ici, on a donné comme **paramètre** à notre fonction getRandomNumber les **valeurs** contenu dans game.min (donc 0) et game.max (donc 500).

## Utiliser un objet en paramètre

Maintenant essayons autre chose !

- On va modifier notre fonction getRandomNumber pour qu'elle prenne en paramètre un **objet**, qui lui même contient des **clés/valeurs** min et max.

![What ?!!!](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExdWF2MDlxYXgwcmozdDU2OWM4cm9tdG5wcXE2cTBmbnJ2am5ibHFkaCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ghuvaCOI6GOoTX0RmH/giphy.gif)

```Javascript 
function getRandomNumber(objet) {
    return Math.floor(Math.random() * (objet.max - objet.min + 1)) + objet.min;
}
```
↑ Ici, on construit simplement notre fonction. Dans sa construction, **on fait comprendre à notre fonction** qu'on lui donnera **toujours** un objet en paramètre et que cet objet contiendra **toujours** une clé/valeur nommé "min" et une autre clé/valeur nommé "max".

- Que se passe-t-il maintenant si on donne notre objet _game_ à notre fonction :

```Javascript
const game = {
    min = 0,
    max = 500,
}

function getRandomNumber(objet) {
    return Math.floor(Math.random() * (objet.max - objet.min + 1)) + objet.min;
}

getRandomNumber(game);
```

Notre fonction getRandomNumber va ici chercher dans notre objet _game_ les **valeurs** contenus dans _game.max_ et _game.min_.

En d'autres termes, elle va remplacer le paramètre "_objet_", le nom générique que l'on a renseigné lors de la construction de notre fonction, et le remplacer par notre paramètre "_game_", notre **objet**.

- Pour imager notre fonction va faire ceci :

```Javascript
return Math.floor(Math.random() * (game.max - game.min + 1)) + game.min;
```
Concrètement, elle a remplacé le mot "objet" par "game", sauf que notre Javascript connaît déjà _game_ et il sait que c'est un **objet**. Il va donc pouvoir remplacer _game.max_ et _game.min_ par leur **valeur** correspondante.


### Mais à quoi ça peut servir ?

- Imaginons qu'on souhaite faire plusieurs difficulté de jeu. Construisons plusieurs objet :

```Javascript 
const gameEasy = {
    min = 0,
    max = 500,
}

const gameMedium = {
    min = 0,
    max = 1000,
}

const gameHard = {
    min = 0,
    max = 10000,
}
```

Et bien maintenant on a simplement à renseigner l'**objet** que l'on veut en paramètre dans notre fonction pour qu'elle nous génère le nombre que l'on veut :

```Javascript 
getRandomNumber(gameEasy);

// ou 

getRandomNumber(gameMedium);

//ou

getRandomNumber(gameHard);
```
Et de la même manière que précédement, notre fonction va aller chercher les valeurs correspondantes pour chacun de nos différents objets "game*".