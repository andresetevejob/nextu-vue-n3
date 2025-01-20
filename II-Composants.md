# Composants

## I - Créer sa première application

### - Pré-requis:
* Nodejs >=20
* Vscode


Nous allons dans cette partie crée notre première application vue-js.

* Créez un dossier de projet dans un repertoire sur votre machine

* Positionnez vous ensuite dans ce projet via le terminal

* Faites la commande npm create vue@latest et remplissez le questionnaire comme sur l'image ci-dessous : 

![alt text for screen readers](/images/vue-scaffold.png)

* Ouvrez le repertoire de projet depuis vs-code

* Créer un fichier dans le repertoire views et nommez le NextuHelloWorldView

* Rajoutez-y le code ci-dessous :
```
<script lang="ts">
import { ref } from 'vue'

export default {
  name: 'NextuHelloWorldView',
  setup() {
    const message = ref('Hello World')
    const updateMessage = () => {
      message.value = 'Change message'
    }
    return {
      message,
      updateMessage,
    }
  },
}
</script>
<template>
  <div>{{ message }}</div>
  <button v-on:click="updateMessage">Change Message</button>
</template>
```

* Ensuite dans le fichier App.vue de votre application, rajoutez le code ci-dessous:
```
<script lang="ts">
import NextuHelloWorldView from './views/NextuHelloWorldView.vue'

export default {
  setup() {
    return {
      NextuHelloWorldView,
    }
  },
  components: {
    NextuHelloWorldView,
  },
}
</script>

<template>
  <main>
    <NextuHelloWorldView />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
```
* Faites un npm i et un npm run dev dans le dossier de votre projet

* Allez dans le navigateur , vous devriez avoir le résultat comme dans l'image ci-dessous:

![alt text for screen readers](/images/hello-world.png)


## II - Structure d'un projet vue-js

![alt text for screen readers](/images/structure-vue-js-project.png)


## III - Anatomie d'un composant vue-js

![alt text for screen readers](/images/component-structure.png)




## IV - Les attributs d'un composants

* Pour definir les attributs d'un composant, il faut utiliser le champ props
```
props: {
    count: {
      type: Number,
      default: 2,
    },
    isActive: {
      type: Boolean,
      default: true,
    },
  },
```
* Utilisation dans le setup
```
 setup(props) {
    const message = ref('Hello World')
    const countData = props.count
    const updateMessage = () => {
      message.value = 'Change message'
    }
    return {
      message,
      countData,
      updateMessage,
    }
},
```
