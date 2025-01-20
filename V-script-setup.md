# Script setup

Vue-js en sa version 3.2 a introduit la notion de script setup
qui est un sucre syntaxique pour le SFC.

qui permet d'avoir :

* moins de code verbeux
* déclarer les props et les evenements en utilisant le pur typescript
* Meilleur performance le modèle est compilé dans la même fonction de rendu sans un proxy intermediaire

* Syntaxe de base 

```
<script setup>
console.log('hello script setup')
</script>
```

* Transformation de notre composant NextuViewHelloWorld avec le sfc

```
<script lang="ts" setup>
import { ref } from 'vue'
const message = ref('Bonjour tout le monde')
const props = defineProps<{
  count: number
}>()
const countData = props.count
</script>

```

vs 

```
<script lang="ts">
import { ref } from 'vue'

export default {
  name: 'NextuViewHelloWorld',
  props: {
    count: {
      type: Number,
      default: 2,
    },
  },
  setup(props) {
    const message = ref('Bonjour tout le monde')
    const countData = props.count
    return {
      message,
      countData,
    }
  },
}
</script>
```

