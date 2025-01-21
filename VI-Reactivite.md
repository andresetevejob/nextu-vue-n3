# La Reactivité

## Presentation du paradigme de la programmation reactive


## Ref

Dans la composition api, la façon de déclarer une donnée réactive se fait au moyen
de la fonction ref(). Cette fonction prend en paramètre un argument et l'envéloppe avec
un objet ayant un attribut value

exple : 
```
const count = ref(0)
// pour accéder à la valeur de count dans la partie script
console.log(count.value)
// néanmoins l'accès via le template se fait sans le .value
{{ count }}
```

* Les objets ref peuvent être mutable au moyen d'évènements

```
 <script lang="ts" setup>
   const count = ref(0)
   const increment = ()=> count.value++
 </script>
 <template>
    <button @click = "increment">increment</button>
    <div>{{count}}</div>
 </template>
```

* Pourquoi avons nous-besoin des objets Refs avec l'attribut .value  ?

Vue-js enveloppe les variables primitives dans un objet avec une propriété .value, car en Javascript, il n'est pas possible de detecter le changement d'une variable primitive, cependant pour un objet, il est possible de detecter les changements de propriétes via les attributs getter et setter

Les variables primitives sont donc enveloppés dans un objet Ref, ci-dessous le pseudo code pour illustré

```
// pseudo code, not actual implementation
const myRef = {
  _value: 0,
  get value() {
    track()
    return this._value
  },
  set value(newValue) {
    this._value = newValue
    trigger()
  }
}
```

Autre point est que contrairement au type primitif, un objet Ref peut être passer à une fonction et vue-js maintient la réactivité dans cette fonction pour garder la dernière valeur de l'objet

exple :
```
<script lang="ts" setup>
import { ref,type Ref } from 'vue'
const count = ref(0)
const count2 = ref(0)
//passage de paramètres d'une valeur réactive à une fonction
//vue conserve la réactivité
const increment = (v:Ref<number>)=> v.value++
const incrementCounter = ()=> increment(count) 
const incrementCounter2 = ()=>increment(count2) 
</script>
<template>
  <div>count 1 : {{ count }}</div>
  <button @click="incrementCounter" type="button">Increment réactif 1</button>
  <div>count 2 : {{ count2 }}</div>
  <button @click="incrementCounter2" type="button">Increment réactif 2</button>
</template>
<style></style>
```

## Reactive 

Cet objet contrairement au Ref permet de gérer la réactivité sur des objets complexes, même si Ref peut le faire, il est préferable d'utiliser Reactive

exple : 
```
import { reactive } from 'vue'
const state = reactive({ count: 0 })

// dans le template
<button @click="state.count++">
  {{ state.count }}
</button>
```
Contrairement aux primitifs, Vue js peut créer des proxy qui detecteront des changements sur les propriétés des objets

exple :

```
<script lang="ts" setup>
import { ref } from 'vue'
const obj = ref({
  nested: { count: 0 },
  arr: ['foo', 'bar']
})
function mutateDeeply() {
  // these will work as expected.
  obj.value.nested.count++
  obj.value.arr.push('baz')
}
</script>
<template>
  <button @click="mutateDeeply">Ajouter de nouveau un element baz dans le tableau</button>  
  <div v-for="(item,i) in obj.arr" :key="i">
    {{item}}
  </div>
</template>

```
* Reactive proxy vs Original

seulement le proxy est réactif, les mutations sur l'objet original ne déclenche pas la mise à jour du DOM

```
<script lang="ts" setup>
import { reactive } from 'vue'
const org = {
  nested: { count: 0 },
  arr: ['foo', 'bar']
}
const obj = reactive(org)
function mutateDeeply() {
  // these will work as expected.
  obj.nested.count++
  obj.arr.push('baz')
}
/**
 * seulement le proxy est réactif, 
 * les mutations sur l'objet original ne déclenche 
 * pas la mise à jour du DOM
 */
function mutateDeeplyOrig() {
  // these will work as expected.
  org.nested.count++
  org.arr.push('baz')
}
</script>
<template>
  <button @click="mutateDeeply">Ajouter de nouveau un element baz dans le tableau</button>  
  <div v-for="(item,i) in obj.arr" :key="i">
    {{item}}
  </div>
  <br/>
  <div>Objet Orignal {{org.nested.count}}</div>
  <button @click="mutateDeeplyOrig">Ajouter de nouveau un element baz dans le tableau original</button>  
  <div v-for="(itemOrg,i) in org.arr" :key="i">
    {{itemOrg}}
  </div>
</template>
```
* Par contre le proxy et l'original ne sont pas égaux 
```
console.log(obj === org) // false
```

## Les types dans la réactivité

* Ref gère l'inférence sur la valeur initial
```
import { ref } from 'vue'

// inferred type: Ref<number>
const year = ref(2025)

// => TS Error: Type 'string' is not assignable to type 'number'.
year.value = '2025'

```
* On peut gérer les types complexes avec 

L'objet Ref

```
import { ref } from 'vue'
import type { Ref } from 'vue'

const year: Ref<string | number> = ref('2025')
// cela est possible à cause du union Type
year.value = 2025 // ok!
```
ou
```
// resulting type: Ref<string | number>
const year = ref<string | number>('2020')
// cela est possible à cause du union Type
year.value = 2020 // ok!
```

* Reactive gère aussi l'inférence de type
```

import { reactive } from 'vue'

// inferred type: { title: string }
const book = reactive({ title: 'Vue 3 Guide' })


```
equivalent 

```
import { reactive } from 'vue'

interface Book {
  title: string
  year?: number
}

const book: Book = reactive({ title: 'Vue 3 Guide' })

```
