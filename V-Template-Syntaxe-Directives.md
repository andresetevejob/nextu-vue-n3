# Template Syntaxe et Directives


### Texte Interpolation 

Afficher les données d'une variable

```
<span>Message: {{ msg }}</span>
```

### Modifier l'attribut d'un élément

```
<div :id="dynamicId"></div>
```

```
<a :href="url"></a>
```

### Les attributs booléens
```
<button :disabled="isButtonDisabled">Button</button>
```

### Structures conditionnelles
  * v-if : 
```
<p v-if="seen">Now you see me</p>
```
Le composant ne sera pas crée dans la page web si la condition n'est pas vérifié

 * v-show :  
Le composant sera crée mais en mode invisible si la condition n'est pas vérifier 


### Itérer sur les éléments 
 * v-for

```
<li v-for="(item,i) in items" :key=1>
  {{ item.message }}
</li>

```

### Gestion des évènements
  #### v-on :
Cette directive permet les interactions avec l'utilisateur de notre application, comme dans toutes applications web, nous avons besoin que notre utilisateur puisse souvent soumettre des données ou faire tout autre action

  * Syntaxe

  ```
    v-on:event = "handler"
    // ou
    @event = "handler"
  ```
 Le gestionnaire d'évènement ou handler event peut être :

  * une instruction javascript qui sera declenché par l'évènement  :
  * un nom de méthode définie dans un composant


```
  // instruction javascript
 // script
  const count = ref(0)
 //Template
   <button @click="count++">Add 1</button>
   <p>Count is: {{ count }}</p>

 ```
 ```

// script
const name = ref('WebTech')

function greet(event) {
  alert(`Hello ${name.value}!`)
  // `event` is the native DOM event
  if (event) {
    alert(event.target.tagName)
  }
}
// Template
<!-- `greet` is the name of the method defined above -->
// le nom greet pointe vers la fonction greet
<button @click="greet">Greet</button>
```
* Appeler une méthode comme gestionnaire d'évènements
```
// script
function saveData(data) {
  alert(`${$data} has been saved`)
}

//Template
<button @click="saveData('data1')">Save data 1</button>
<button @click="saveData('data2')">Save data 2</button>

```

* Avoir accès à l'évènement declencheur du handler
```
// script
function warn(message, event) {
  // now we have access to the native event
  if (event) {
    event.preventDefault()
  }
  alert(message)
}

//Template
<!-- using $event special variable -->
<button @click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

<!-- using inline arrow function -->
<button @click="(event) => warn('Form cannot be submitted yet.', event)">
  Submit
</button>

```

* Les modificateurs d'évènements 

IL est aussi possible d'avoir accès aux modificateurs d'évènements via la directive
```
<!-- the click event's propagation will be stopped -->
<a @click.stop="doThis"></a>
<!-- the submit event will no longer reload the page -->
<form @submit.prevent="onSubmit"></form>

```


* Event Bubbling
"Bubble up" (ou remontée d'événements) fait référence au processus où un événement est déclenché dans un composant enfant et "remonté" vers le composant parent. Cependant, parfois cela peut poser des problèmes si la gestion des événements n'est pas correctement structurée, ce qui peut entraîner une confusion ou une logique difficile à maintenir.

comment stopper le bubble up lors d'un clique sur le composant enfant

```
// script
const save = ()=>{
  console.log("parent call");
}
const saveName = (name:string,event:Event)=>{
 console.log(`Hi ${name}`);
 event.stopPropagation(); // empêche la propagation de l'évènement vers le conteneur
}
// Template
<div @click="save()">
   <button @click="saveName('Bob', $event)">Save</button>
</div>
```
  