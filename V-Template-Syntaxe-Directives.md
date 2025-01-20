# Template Syntaxe 


* Texte Interpolation 

Afficher les données d'une variable

```
<span>Message: {{ msg }}</span>
```

* Modifier l'attribut d'un élément

```
<div :id="dynamicId"></div>
```

```
<a :href="url"></a>
```

* Les attributs booléens
```
<button :disabled="isButtonDisabled">Button</button>
```

* Structures conditionnelles
  * v-if : 
```
<p v-if="seen">Now you see me</p>
```
Le composant ne sera pas crée dans la page web si la condition n'est pas vérifié

 * v-show :  
Le composant sera crée mais en mode invisible si la condition n'est pas vérifier 


* Itérer sur les éléments 
 * v-for

```
<li v-for="item in items">
  {{ item.message }}
</li>

```
