# Formulaire

## La directive v-model

Cette directive permet une liaison  entre le composant html et le code javascript et vice versa.
Cela signifie qu'une modification depuis le js impactera la vue et vice versa

exple :
```
<input v-model="text">
```

Cette directive peut être utilisée avec les différents composants html suivants : 
* input
* textarea
* radio
* checkbox
* select

## checkbox
```
<input type="checkbox" id="checkbox" v-model="checked" />
<label for="checkbox">{{ checked }}</label>
```

Multiple checkbox

```
<div>Checked names: {{ checkedNames }}</div>

<input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
<label for="jack">Jack</label>

<input type="checkbox" id="john" value="John" v-model="checkedNames" />
<label for="john">John</label>

<input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
<label for="mike">Mike</label>

```