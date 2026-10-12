---
title: Démonstration
---
# Les évolutions de la syntaxe depuis ES5

Depuis la version 5 de ECMAScript (et surtout avec la version 6), la syntaxe du langage a beaucoup évolué pour aller vers une meilleure cohérence et une meilleure robustesse dans le code produit. Ce chapitre résume les évolutions les plus importantes.

## Le mode strict (ES5)

Depuis ES5, il existe un mode strict qui active un renforcement des contrôles par l’interpréteur. Ce mode permet d’éviter un certain nombre d’erreurs de programmation. Pour des raisons de rétro-compatibilité, ce mode n’est pas actif par défaut. Cependant, il est très fortement conseillé de l’activer pour tout nouveau développement.

Pour activer le mode strict, il suffit de placer au début du fichier source la chaîne de caractères :
```javascript
'use strict'
```

En mode strict, il n’est pas possible d’utiliser une variable qui n’a pas été préalablement déclarée (avec les mots-clés `var`, `let` ou `const`). Cela évite ainsi les bugs dus à des erreurs de typo.

En mode strict, l’usage du mot-clé `with` est impossible.

## Déclarer une variable avec let et const (ES6)

Le mot-clé var est utilisé en JavaScript pour déclarer des variables.

```javascript
var i = 0;
```
Cependant la notion de déclaration de variable est particulière en JavaScript par rapport à la plupart des autres langages de programmation proches. `var` n’empêche pas de déclarer à nouveau une variable avec le même nom et la portée des variables est particulière à JavaScript. Si la variable est déclarée au plus haut niveau, il s’agit d’une variable globale mais si elle déclarée ailleurs, sa portée correspond à la fonction dans laquelle elle est déclarée. Cela peut entraîner des effets de bord difficiles à comprendre :
	
```javascript title="demo" hl_lines="6-8"
var variable_globale = "globale";

function ma_fonction() {

    var variable_locale = "locale";
    if (true) {
        var variable_locale_2 = "locale 2";
    }
    console.log(variable_globale);
    console.log(variable_locale);
    console.log(variable_locale_2);
}

ma_fonction();
// Affiche
// globale
// locale
// locale 2
```

À la ligne 7, la variable variable_locale_2 est déclarée dans le bloc if mais, contrairement à d’autres langages de programmation, la portée de cette variable est la fonction. Donc il est possible d’accéder à sa valeur à la ligne 11 après le bloc if.

Pour corriger ce comportement tout en maintenant la rétro-compatibilité pour le code existant, ES6 introduit le mot-clé let.
```javascript
let j = 0;
```
Une variable déclarer avec let ne peut pas être déclarée à nouveau et sa portée est limitée au bloc dans lequel elle est déclarée.

Important

Pour tout nouveau code, il est recommandé d’utiliser let pour déclarer toutes les variables.

Avec ES6, on dispose également du mot-clè const pour garantir que la déclaration est constante.

const pi = 3.1416;

La structure for … of (ES6)

Une nouvelle structure de contrôle for a été ajoutée avec ES6 pour permettre de parcourir les objets itérables. Il s’agit de la structure for ... of

for (let v of voyelles) {
    console.log(v);
}

// Affiche
// a
// e
// i
// o
// u
// y

Les tableaux et les chaînes de caractères sont des objets itérables. Il est donc très facile de les parcourir avec cette nouvelle structure de contrôle.

for (let i of [1, 2, 3, 4]) {
    console.log(i);
}

for (let l of "Bonjour") {
    console.log(l);
}

Note

Nous reviendrons dans un chapitre ultérieur sur la notion d’itérateur et nous verrons comment créer nos propres itérateurs.
Gabarit de chaîne de caractères (ES6)

ES6 introduit les gabarits de chaîne de caractères (template string) pour formater plus facilement des données dans des chaînes de caractères. Plutôt que d’utiliser l’opérateur + de concaténation :

let a = 1;
let b = 2;
let message = "La somme de " + a + " et de " + b + " est " + (a + b) + ".";

On peut utiliser le caractère ` pour délimiter la chaîne de caractères et préciser les noms des variables avec ${} :

let a = 1;
let b = 2;
let message = `La somme de ${a} et de ${b} est ${a + b}`;

La syntaxe est plus concise et bien plus lisible. La valeur donnée avec ${} peut être une expression complète : un appel de fonction, l’attribut d’un objet…

let message = `La circonférence d'un cercle de rayon 3 est ${(2 * Math.PI * 3).toFixed(3)}`;
console.log(message); // Affiche La circonférence d'un cercle de rayon 3 est 18.850

L’utilisation du caractère ` pour délimiter une chaîne de caractères permet également d’écrire cette chaîne sur plusieurs lignes :

let message = `Ceci est un message.
Ce message est sur plusieurs lignes.
Il sera affiché également sur plusieurs lignes.`;

console.log(message);

// Affiche :
// Ceci est un message.
// Ce message est sur plusieurs lignes.
// Il sera affiché également sur plusieurs lignes.

Valeur par défaut des paramètres (ES6)

Depuis ES6, il est possible de fournir des valeurs par défaut aux paramètres d’une fonction.

function saluer(qui, message = "Bonjour") {
    console.log(message, qui);
}

saluer("David"); // Affiche Bonjour David
saluer("David", "Bonsoir"); // Affiche Bonsoir David

Le paramètre de reste (ES6)

Avec l’opérateur ..., il est possible de déclarer une liste quelconque de paramètres correspondant au reste des paramètres. Cette liste sera vue comme un tableau à l’intérieur de la fonction

function additionner(x1, x2, ...autres) {
    let resultat = x1 + x2;
    for (let n of autres) {
        resultat += n;
    }
    return resultat;
}

console.log(additionner(1, 2));
// Affiche 3
console.log(additionner(1, 2, 4));
// Affiche 7
console.log(additionner(1, 2, 4, 8));
// Affiche 15

Note

Si une fonction ne prend qu’un paramètre de reste :

function maFonction(...args) {
    console.log(args);
}

Cela est équivalent à utiliser la variable implicite arguments :

function maFonction() {
    console.log(arguments);
}

Cependant, le recours à l’opérateur ... dans la signature améliore la compréhension de la fonction.
La décomposition de tableau (ES6)

L’opérateur ... sert également à la décomposition de tableau qui permet de passer les paramètres à l’appel d’une fonction sous la forme d’un tableau.

let args = [2, 3];

function additionner(x, y) {
    console.log(x + y);
}

additionner(...args); // Affiche 5

Note

Auparavant, ce type d’appel était possible en utilisant la méthode apply d’une fonction :

let args = [2, 3];

function additionner(x, y) {
    console.log(x + y);
}

additionner.apply(null, args); // Affiche 5

L’affectation de tableau par décomposition (ES6)

L’affectation par décomposition (destructuring assignment) permet de réaliser des affectations multiples à partir d’un tableau.

On peut déclarer un tableau de variables à gauche de l’affectation.

const tableau = [1, 2, 3];
let [a, b, c] = tableau;
console.log(a); // Affiche 1
console.log(b); // Affiche 2
console.log(c); // Affiche 3

Nous pouvons utiliser cette syntaxe pour intervertir la valeur de deux variables.

let a = 1:
let b = 2:
[a, b] = [b, a]; // a vaut 2 et b vaut 1

Le tableau à gauche de l’affectation peut avoir une taille différent du tableau à droite de l’affectation. Si le tableau à gauche est plus petit, les éléments en plus à droite ne sont pas pris en compte.

let [a, b] = [1, 2, 3, 4]; // a vaut 1 et b vaut 2

Si le tableau à gauche de l’affectation est plus grand, les éléments en plus reçoivent la valeur undefined.

let [a, b, c, d] = [1, 2]; // a vaut 1, b vaut 2, c et d valent undefined

On peut utiliser l’opérateur de reste ... pour affecter à une variable tous les éléments restant :

let [a, ...b] = [1, 2, 3, 4]; // a vaut 1 et b vaut [2, 3, 4]

L’affectation d’objet par décomposition (ES6)

L’affectation par décomposition (destructuring assignment) permet également de réaliser des affectations multiples à partir d’un objet. Dans ce cas, le nom des variables à gauche de l’affectation correspondent au nom des propriétés de l’objet.

const personne = {
    prenom: "David",
    nom: "Gayerie"
};

let {nom, prenom} = personne;
console.log(prenom); // Affiche David
console.log(nom); // Affiche Gayerie

Comme pour l’affectation de tableau par décomposition, on peut spécifier moins de variables à gauche ou plus de variables ou utiliser l’opérateur de reste ... pour affecter les propriétés restantes sous la forme d’un nouvel objet.

const personne = {
    prenom: "David",
    nom: "Gayerie",
    taille: 174
};

let {nom, prenom} = personne; // nom vaut "David" et prenom vaut "Gayerie"

const personne = {
    nom: "Gayerie",
};

let {nom, prenom} = personne; // nom vaut "David" et prenom vaut undefined

const personne = {
    prenom: "David",
    nom: "Gayerie",
    taille: 174
};

let {taille, ...nomComplet} = personne; // taille vaut 174
                                        // nomComplet vaut {prenom: "David", nom: "Gayerie"}

L’opérateur d’exponentiation (ES7)

ECMAScript 7 a introduit l’opérateur d’exponentiation ** qui se comporte comme un appel à Math.pow.

const carre = 4 ** 2; // produit 16
const cube = 4 ** 3; // produit 64

Le code ci-dessus est strictement équivalent à

const carre = Math.pow(4, 2); // produit 16
const cube = Math.pow(4, 3); // produit 64

Programmation asynchrone avec async et await (ES7)

ECMAScript 7 a ajouté les mots-clés aync et await pour faciliter la programmation asynchrone. Nous verrons plus en détail l’utilisation de ces mots-clés dans un chapitre ultérieur.
Opérateur de coalescence des valeurs nulles (ES11)

ECMAScript 11 a introduit l’opérateur ?? qui est appelé l’opérateur de coalescence des valeurs nulles (nullish coalescing operator). Il permet de fournir une valeur alternative lorsqu’une expression vaut null ou undefined.

let x = null ?? "valeur par défaut";      // x vaut "valeur par défaut"
let y = undefined ?? "valeur par défaut"; // y vaut "valeur par défaut"
let z = "hello" ?? "valeur par défaut";   // z vaut "hello"

Avant l’apparition de cette opérateur, les développeurs JavaScript avaient l’habitude d’utiliser l’opérateur logique || pour réaliser un traitement similaire :

let x = null || "valeur par défaut";      // x vaut "valeur par défaut"
let y = undefined || "valeur par défaut"; // y vaut "valeur par défaut"
let z = "hello" || "valeur par défaut";   // z vaut "hello"

Cependant les deux opérateurs ne sont pas identiques dans leur comportement. L’opérateur logique || retourne l’opérande de droite si l’opérande de gauche est faux. Or, en JavaScript, il n’y a pas que null et undefined qui s’évaluent à faux.

let m = false || "valeur par défaut"; // x vaut "valeur par défaut"
let n = false ?? "valeur par défaut"; // y vaut false

let x = 0 || "valeur par défaut";  // x vaut "valeur par défaut"
let y = 0 ?? "valeur par défaut";  // y vaut 0

let w = "" || "valeur par défaut"; // x vaut "valeur par défaut"
let z = "" ?? "valeur par défaut"; // y vaut ""

Chaînage optionnel (ES11)

Il est très courant de chaîner les références pour une meilleure lisibilité du code :

let x = personne.adresse.rue;

Le problème avec le code ci-dessus, c’est que nous devons être sûr que la propriété adresse existe et possède une valeur définie sinon cette expression échouera avec une erreur du type :

TypeError: Cannot read property 'adresse' of undefined

Pour écrire du code robuste, nous pouvons vérifier préalablement que cette propriété existe ou, avec ES11, nous pouvons utiliser l’opérateur de chaînage optionel ?. :

const x = personne.adresse?.rue;

Si adresse vaut null ou undefined, l’évaluation de l’expression s’arrête sans erreur et produit la valeur undefined.

const personne = {};

console.log(personne.adresse?.rue); // Affiche "undefined"

Il est également possible d’utiliser cet opérateur pour l’appel de méthode. Si la méthode n’existe pas, l’expression produit également la valeur undefined.

const personne = {
    parler: function() {
        return "bonjour";
    }
};

console.log(personne.parler?.()); // Affiche "bonjour"
console.log(personne.crier?.()); // Affiche "undefined"

Prudence

Le chaînage optionnel ne s’applique pas sur la première référence de la chaîne.

console.log(personne?.nom);

L’utilisation de l’opérateur ?. sur la variable personne n’a aucun effet. Si personne vaut null ou undefined, ce programme échouera :

Uncaught ReferenceError: personne is not defined

