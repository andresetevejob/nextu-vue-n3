# Typescript

## I -  Presentation

## II  - Les types de données

### 1 - Les types primitifs

* string : chaîne de caractère exple: "bonjour"
* number : correspond aux nombres exple : 42
* boolean : true et false

```
Les noms de types String, Number, et Boolean (avec une première lettre majuscule) existent, mais réfèrent à des types spéciaux qui vont très rarement apparaître dans votre code. Utilisez toujours string, number, ou boolean pour annoter vos types.

```

### 2 - Les tableaux

Définition d'un tableau exple :

```
let x  = [1,2,3]

```
On peut définir un tablea d'un type en suivant la syntaxe 
```
type[]
```
Exemple un tableau de nombre
let x : number[]

### 3 - Le type any
C'est un type spécial qui peut contenir n'importe quel type de valeur

```
let obj: any = { x: 0 };
// Aucune de ces lignes ne va émettre d'erreur.
// Utiliser `any` désactive toute vérification de types, et TypeScript supposera
// que vous connaissez l'environnement mieux que lui.
obj.foo();
obj();
obj.bar = 100;
obj = "hello";
const n: number = obj;

```
NB : Faire attention à l'utilisation de ce type dans vos projets

### 4 - Les fonctions

Syntaxe : 
```
function name(parameters:types):returnType{
    //other code
}
```
Exple : 
```
function greet(name:string){
    return `Hello ${name}`;
}
```
* fonction anonyme
```
const names = ["Alice", "Bob", "Eve"];
// Typage contextuel pour des fonctions
names.forEach(function (s) {
  console.log(s);
})
```

* fonction flèchée : 
```
const helloWorld = ()=>{
  return "bonjour"
}
```

### 5 - Les interfaces
```
interface MonInterface{
 name: string,
 age: number
}
```

### 6 - Les Types unions

Un type union est un type formé de deux ou plusieurs types, représentant des valeurs qui pourraient faire partie de n’importe lequel de ces types.

```
function printId(id: number | string) {
  console.log("Votre ID est : " + id);
}
// OK
printId(101);
// OK
printId("202");
// Erreur
printId({ myID: 22342 });
```

## III - Les fonctionnalités de typescript

Dans cette partie nous présenterons certaines fonctionnalités de typescript.

### 1 - Les optionals arguments
```
function addPointsToScore(player: HasScore, points?: number): void {
  points = points || 0;
  player.score += points;
}
```


### 2 - Type guard avec l'operateur in

Récuperer le type d'une variable notamment
dans un block conditionnel

```
function StudentId(x: string | number) {
    if (typeof x == 'string') {
        console.log('Student');
    }
    if (typeof x === 'number') {
        console.log('Id');
    }
}
StudentId(`446`); //prints Student
StudentId(446); //prints Id
```


 