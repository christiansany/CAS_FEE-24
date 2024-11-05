# Vue.js Miniintro

## Inhalt

* [Was ist Vue.js?](#was-ist-vuejs)
* [Quickstart](#quickstart)
* [Dekleratives Rendering](#dekleratives-rendering)
* [User Input](#user-input)
* [Conditionals and Loops](#conditionals-and-loops)
* [Components](#components)
* [Vorteile von Vue.js](#vorteile-von-vuejs)

## Was ist Vue.js?

> Vue (pronounced /vjuː/, like **view**) is a **progressive framework** for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable. The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects. On the other hand, Vue is also perfectly capable of powering sophisticated Single-Page Applications when used in combination with modern tooling and supporting libraries.

## Quickstart

Der einfachste Weg zum ausprobieren ist, [Vue.js](https://vuejs.org/) per [StackBlitz](https://vite.new/vue-ts) zu nutzen (nutzt [Vite](https://vite.dev/guide/)).  
Als Alternative kann man auch einfach ein neues Projekt lokal aufsetzen mit [Vite](https://vite.dev/guide/).

**Demo** 🤯

- [Vue.js Demo](https://stackblitz.com/edit/vitejs-vite-v9sapd)

## Dekleratives Rendering

Im Herzen von Vue ist ein System, welches das Deklarative Rendering ermöglicht. Wie im ersten Beispiel ersichtlich, ist die Template Syntax einfach zu verstehen.
Dabei sind unsere Variablen [**reactive**](https://vuejs.org/guide/extras/reactivity-in-depth.html). Dies bedeutet, dass alle Änderungen an unserem internen State selbständig im DOM angepasst werden.

```vue
<script setup lang="ts">
import { ref } from 'vue';

const counter = ref(0);

setInterval(() => {
  // No setState needed, we can directly manipulate the value and Vue will update the DOM
  counter.value++;
}, 1000);
</script>

<template>
  <p>Counter: {{ counter }}</p>
</template>
```

**Demo** 🤯

- [Dekleratives Rendering](https://stackblitz.com/edit/vitejs-vite-iowb8f)

Im Beispiel nutzen wir [`ref`](https://vuejs.org/api/reactivity-core.html#ref), um eine Referenz zu erstellen. Dies ist notwendig, damit Vue weiss, dass sich der Wert geändert hat und das DOM aktualisiert werden muss. Bei React kann man dies als eine Kombination von `useState` und `useRef` sehen.

Vue nutzt sogenannte [Singe-File Components (SFC)](https://vuejs.org/guide/scaling-up/sfc.html). Diese bestehen aus drei Teilen:
1. **Script**: JavaScript-Code
2. **Template**: HTML-Code
3. **Style**: CSS-Code

## Directives

In Vue gibt es sogenannte [Directives](https://vuejs.org/api/built-in-directives.html). Diese sind spezielle Attribute, die wir in unserem HTML-Code verwenden können. Sie beginnen immer mit `v-`, aber für ein paar gibt es auch shorthands. Wer bereits mit Angular gearbeitet hat, wird sich hier wiederfinden.

So kann man z.B. mit der [`v-bind` Directive](https://vuejs.org/api/built-in-directives.html#v-bind) variablen an Attribute knüpfen/übergeben.

```vue
<script setup lang="ts">
const message = 'Hello World';
</script>

<template>
  <p v-bind:title="message">
    Hover your mouse over me for a few seconds to see my dynamically bound
    title!
  </p>
  <br />Same same
  <p :title="message">
    Hover your mouse over me for a few seconds to see my dynamically bound
    title!
  </p>
  <br />Stringinterpolation
  <p :title="'Hello, ' + message">
    Hover your mouse over me for a few seconds to see my dynamically bound
    title!
  </p>
</template>
```

**Demo** 🤯

- [Binding Attributes](https://stackblitz.com/edit/vitejs-vite-rwrqrm?file=src%2FApp.vue)

**Hilfreiche Links**

* [Reactivity in Depth 🔥](https://vuejs.org/guide/extras/reactivity-in-depth.html)

## User Input

Die Events, die von unserem UI abgeschossen werden, können mit der `v-on` [Directive](https://vuejs.org/api/built-in-directives.html#v-on) abgefangen werden.  
Auch hier gibt es eine gekürzte Version mit `@`.

```vue
<script setup lang="ts">
import { ref } from 'vue';

const counter = ref(0);

const increment = () => {
  counter.value++;
};
</script>

<template>
  <button @click="increment">Add 1</button>
  <p>Count is: {{ counter }}</p>
</template>
```

Hier sind ebenfalls die Ähnlichkeiten mit React zu erkennen.

**Demo** 🤯

- [Eventhandling](https://stackblitz.com/edit/vitejs-vite-pbpnkk?file=src%2FApp.vue)

### Two-Way Databinding

Mit der `v-model` [Directive](https://vuejs.org/api/built-in-directives.html#v-model) können wir unseren State von den Komponenten direkt durch das UI manipulieren.

```vue
<script setup lang="ts">
import { ref } from 'vue';
const message = ref();
</script>

<template>
  <p>Message: {{ message }}</p>
  <input v-model="message" />
</template>
```

**Demo** 🤯

- [Two-Way Databinding](https://stackblitz.com/edit/vitejs-vite-8skfd5?file=src%2FApp.vue)

## Conditionals and Loops

### Konditionales Rendering

Konditionales Rendering ist sehr einfach zu implementieren mit der [`v-if`](https://vuejs.org/api/built-in-directives.html#v-if) Directive. Diese kann ebenfalls mit [`v-else-if`](https://vuejs.org/api/built-in-directives.html#v-else-if) und/oder [`v-else`](https://vuejs.org/api/built-in-directives.html#v-else) kombiniert werden. Bei der Verwendung dieser Directives wird das Element aus dem DOM entfernt, solange es nicht angezeigt wird.  
Mit der [`v-show`](https://vuejs.org/guide/essentials/conditional.html#v-show) Directive kann ein Element mit `display: none;` lediglich ausgeblendet werden. Somit bleibt es im DOM vorhanden.

Die Elemente die dabei angezeigt bzw. ausgeblendet werden, können dazu animiert werden. Siehe dafür die Dokumentation für die [Transitions](https://vuejs.org/guide/built-ins/transition.html#transition).

```vue
<script setup lang="ts">
import { ref } from 'vue';
const showText = ref(false);
</script>

<template>
  <button @click="showText = !showText">Toggle Text</button>
  <p v-if="showText">Hello there</p>
</template>

```

**Demo** 🤯

- [Konditionales Rendering](https://stackblitz.com/edit/vitejs-vite-rxlwxz?file=src%2FApp.vue)

### Loops

Mit der [`v-for`](https://vuejs.org/api/built-in-directives.html#v-for) Directive können wir durch Arrays oder auch Objekte loopen. Dabei wir die Direktive auf dem Element angebracht, welches wiederholt werden soll.  
Mehr zum Rendering von Listen findest Du [hier](https://vuejs.org/guide/essentials/list.html).

```vue
<script setup lang="ts">
const todos = [
  { text: 'Learn JavaScript' },
  { text: 'Learn Vue' },
  { text: 'Build something awesome' },
];
</script>

<template>
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</template>
```

**Demo** 🤯

- [Loops](https://stackblitz.com/edit/vitejs-vite-pdmxde?file=src%2FApp.vue)

## Components

Vue.js ist gleich wie andere MV*-Frameworks aufgebaut, so dass man sein Widget/Webapp oder ähnliches in verschiedenen Komponenten aufsplitten kann. Diese können ebenfalls ineinander verschachtelt werden.  
Dabei verhält sich Vue.js wiederum sehr ähnlich zu React. Wir können also einfach Komponenten definieren und diese in anderen Komponenten verwenden.

```vue
<!-- EchoMessage.vue -->
<script setup lang="ts">
// defineProps is a helper function that defines props for the component
// https://vuejs.org/api/sfc-script-setup.html#defineprops-defineemits
const { message } = defineProps({
  message: String,
});
</script>

<template>
  <p>{{ message }}</p>
</template>
```

```vue
<!-- App.vue -->
<script setup lang="ts">
import EchoMessage from './components/EchoMessage.vue';
const msg = 'Message from child 2';
</script>

<template>
  <h1>Hello World</h1>
  <EchoMessage message="Message from child 1" />
  <EchoMessage :message="msg" />
</template>
```

**Demo** 🤯

- [Components](https://stackblitz.com/edit/vitejs-vite-2jl5ef?file=src%2Fcomponents%2FEchoMessage.vue,src%2FApp.vue)

### Practice 🔥

Öffne diesen [**StackBlitz**](https://stackblitz.com/edit/vitejs-vite-bn7xjw?file=src%2FApp.vue) als Startpunkt.

Füge die fehlende Funktionalität hinzu, damit unsere Todo-App deployt werden kann.
 
Zeit: ~ 15 min

**Solution**: [https://stackblitz.com/edit/vitejs-vite-ryxwzs](https://stackblitz.com/edit/vitejs-vite-ryxwzs?file=src%2FApp.vue)

## Weiterführende Themen

* [Getting started Guide](https://vuejs.org/guide/introduction.html)
* [Single File Components 🔥](https://vuejs.org/guide/scaling-up/sfc.html)
* [Composition API 🔥](https://vuejs.org/guide/extras/composition-api-faq.html)
* [Vite - Next Generation Frontend Tooling 🔥](https://vite.dev)
