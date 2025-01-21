# COMPUTED ET WATCH

## I -  Computed properties

### 1  - Presentation

Les computed properties permettent dans d'encapsuler une logique qui sera reutilisable dans le template du composant.
Tout comme les objets Ref, le retour généré par un computed properties est accessible via la propertie value au sein du script

```
<script setup>
import { reactive, computed } from 'vue'

const author = reactive({
  name: 'John Resig',
  posts: [
    'IA - Innovation',
    'OLLAMA and Vue-js - LLM in Frontend',
    'RAG - LLM with MONGODB store'
  ]
})

// a computed ref
const publishedPostsMessage = computed(() => {
  return author.posts.length > 0 ? 'Yes' : 'No'
})
// récuperation de la valeur via .value
console.log(publishedPostsMessage.value)
</script>

<template>
  <p>Has published posts:</p>
  <span>{{ publishedPostsMessage }}</span>
</template>

```

Une computed propeties track les dépendances réactives pour mettre à jour le résultat du calcul

### 2 - Computed vs Properties

#### Computed : 
- Gère la mémorisation, c'est à dire tant que les dépendances ne changent pas le
calcul ne se refait pas.Très utiles pour des dépendnances réactives ou le calcul est coûteux

#### Method : 
- Chaque appèle de la méthode nécessite un récalcul même si les dépendnances
n'ont pas changées

```

```

## II - Watch

### 1 - Watch

Les computed properties permettent de calculer des données dérivées de propriétés reactive, dans certains on aura besoin de déclencher une action suite à une modification d'un état

```
<script setup>
import { ref, watch } from 'vue'

const brancheGit = ref('')
const lastCommit = ref('')
const loading = ref(false)

// watch works directly on a ref
watch(brancheGit, async (newBranch, oldBranch) => {
  if (newQuestion.includes('?')) {
    loading.value = true
    lastCommit.value = 'Thinking...'
    try {
      const res = //pseudo call
      lastCommit.value = (await res.json()).commit
    } catch (error) {
      lastCommit.value = 'Error! Could not reach the API. ' + error
    } finally {
      loading.value = false
    }
  }
})
</script>

<template>
  <p>
    Branche:
    <input v-model="brancheGit" :disabled="loading" />
  </p>
  <p>{{ lastCommit }}</p>
</template>

```

* Cas d'utilisation
```
const x = ref(0)
const y = ref(0)

// single ref
watch(x, (newX) => {
  console.log(`x is ${newX}`)
})

// getter
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum}`)
  }
)

// array of multiple sources
watch([x, () => y.value], ([newX, newY]) => {
  console.log(`x is ${newX} and y is ${newY}`)
})

```
Ne peut pas tracker un objet d'une propriété réactive
```
const obj = reactive({ count: 0 })

// this won't work because we are passing a number to watch()
watch(obj.count, (count) => {
  console.log(`Count is: ${count}`)
})

```
En lieu et place utiliser le getter
```
// instead, use a getter:
watch(
  () => obj.count,
  (count) => {
    console.log(`Count is: ${count}`)
  }
)
```
Surveillance profonde l'option deep

* Tout l'objet est observé
```
const obj = reactive({ count: 0 })

watch(obj, (newValue, oldValue) => {
  // fires on nested property mutations
  // Note: `newValue` will be equal to `oldValue` here
  // because they both point to the same object!
})

obj.count++
```

* surveiller des sous propriétés
```
watch(
  () => state.someObject,
  () => {
    // déclencher uniquement que quand someObject state est modifié
  }
)
```

* surveiller les sous propriétés ou objet

```
watch(
  () => state.someObject,
  (newValue, oldValue) => {
    // Note: `newValue` sera ici égal à  `oldValue`
    // *à moins que* state.someObject ait été remplacé
  },
  { deep: true }
)

```

* Les autres options
- eager
- once 


### 2 - WatchEffect

Permet d'observer toutes les propriétés réactives présentes dans le 
corps de la fonction de déclencheuse

```
const todo = ref('')
const status=  ref(false)
watchEffect(async () => {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}&status=${status}`
  )
  data.value = await response.json()
})
```
