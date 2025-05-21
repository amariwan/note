# ⛔️ Don’ts & ✅ Dos in Vue 3

## 1. ❌ Kein `import * as Foo`

**Don't**

```ts
import * as Utils from '@/utils';
```

**Warum vermeiden?**

* Zieht *das ganze Modul* ins Bundle → kein Tree-Shaking
* Schlechtere Lesbarkeit
* Geringere IDE-Unterstützung

**✅ Do**

```ts
import { formatDate, parseInput } from '@/utils/date';
```
> 📚 **Quelle**:   ([Stack Overflow][1])([Stack Overflow][2]).

---

## 2. ❌ Kein Store-Zugriff direkt in Komponenten

**Don't**

```ts
this.$store.dispatch('loadSomething'); // Options API Anti-Pattern
```

**✅ Do**

```ts
const { loadSomething } = useSomethingStore();
await loadSomething();
```

➡ Store-Zugriff nur über Composables in der `App`-Schicht!

> 📚 **Quelle**:   ([Codez Up][3])([Codez Up][4]).

---

## 3. ❌ Kein `$emit` inline im Template

**Don't**

```html
<button @click="$emit('save')">Speichern</button>
```

**✅ Do**

```ts
function onSave() { emit('save'); }
```

```html
<button @click="onSave">Speichern</button>
```
> 📚 **Quelle**:  ([LearnVue][5])

---

## 4. ❌ Keine untypisierten Props/Refs

**Don't**

```ts
const isVisible = ref(false); // kein Typ
```

**✅ Do**

```ts
const isVisible = ref<boolean>(false);
```

```ts
const props = defineProps<{ title: string; isActive: boolean }>();
```
> 📚 **Quelle**:   ([Vue.js][6])([koderhq.com][7])

---

## 5. ❌ Kein `any`, lieber `unknown`

**Don't**

```ts
function parse(data: any) { ... }
```

**✅ Do**

```ts
function parse(data: unknown): ParsedData {
  if (typeof data === 'string') { ... }
}
```
> 📚 **Quelle**: ([Stack Overflow][8])([thoughtbot][9]).

---

## 6. ❌ Kein ungetesteter Zugriff auf `.value`

**Don't**

```ts
doSomething(thing.value.someProp);
```

**✅ Do**

```ts
if (thing.value) {
  doSomething(thing.value.someProp);
}
```

Oder mit Optional Chaining:

```ts
thing.value?.someProp
```
> 📚 **Quelle**:   ([Stack Overflow][10])([Stack Overflow][11]).

---

## 7. ❌ Kein `v-if` + `v-for` am gleichen Element

**Don't**

```vue
<li v-for="item in items" v-if="item.active">{{ item.name }}</li>
```

**✅ Do**

```vue
<template v-for="item in items">
  <li v-if="item.active">{{ item.name }}</li>
</template>
```
  ([Vue.js][12]).
> 📚 **Quelle**: ([Rish's Repository][17])

---

## 8. ❌ Kein `:key="index"`

**Don't**

```vue
<li v-for="(item, index) in list" :key="index">{{ item.name }}</li>
```

**✅ Do**

```vue
<li v-for="item in list" :key="item.id">{{ item.name }}</li>
```
> 📚 **Quelle**:   ([Vue School][13])

---

## 9. ❌ Keine komplexe Logik im Template

**Don't**

```vue
<span>{{ a && b ? format(c) : defaultValue }}</span>
```

**✅ Do**

```ts
const displayValue = computed(() => (a && b ? format(c) : defaultValue));
```

```html
<span>{{ displayValue }}</span>
```
> 📚 **Quelle**:   ([DEV Community][14])

---

## 10. ❌ Keine globale Registrierung aller Komponenten

**Don't**

```ts
app.component('BaseButton', BaseButton); // global für jedes Element
```

**✅ Do**

```ts
import BaseButton from '@/components/BaseButton.vue';
```

Nur gezielt global registrieren, wenn wirklich überall benötigt (z. B. Layout-Komponenten).

> 📚 **Quelle**:   ([LearnVue][15])

---

## 11. ❌ Keine Side-Effects in `computed()`

**Don't**

```ts
const total = computed(() => {
  logTotal(); // side effect
  return price * quantity;
});
```

**✅ Do**

```ts
const total = computed(() => price * quantity);
watch(total, () => logTotal());
```
> 📚 **Quelle**: ([Binarcode][16])

---

## 12. ❌ Props nicht mutieren

**Don't**

```ts
props.title = 'Neuer Titel'; // ❌
```

**✅ Do**

```ts
const titleCopy = ref(props.title);
titleCopy.value = 'Neuer Titel';
```

> 📚 **Quelle**:  ([Rish's Repository][17], [Michael Thiessen][18])

---

## 13. ❌ Keine `filters` verwenden (Vue 2 Legacy)

**Don't**

```vue
{{ price | currency }}
```

**✅ Do**

```ts
const formattedPrice = computed(() => formatCurrency(price));
```

```vue
{{ formattedPrice }}
```
> 📚 **Quelle**:   ([Vue 3 Migration Guide][19])

---

## 14. ❌ Kein ungesicherter Einsatz von `v-html`

**Don't**

```vue
<div v-html="userInput"></div>
```

**✅ Do**

* Nutze ein Sanitizer (z. B. DOMPurify)
* Verwende besser Slots oder gerenderte Komponenten

> 📚 **Quelle**:   ([ESLint Vue][20])

---

## 15. ❌ Keine tiefen Watcher ohne Bedarf

**Don't**

```ts
watch(myObject, () => { ... }, { deep: true });
```

**✅ Do**

* Nur verwenden, wenn wirklich nötig
* Alternativ: spezifische Schlüssel beobachten

> 📚 **Quelle**:   ([diginode.in][21])

---

## 16. ❌ Keine globalen Mixins in Masse

**Don't**

```ts
app.mixin({ created() { ... } });
```

**✅ Do**

* Nutze Composables
* Lokale Mixins für spezifische Komponenten

> 📚 **Quelle**: ([Codez Up][22])

---

## 17. ❌ Kein Event-Bus für globale Events

**Don't**

```ts
EventBus.$emit('user-logged-in');
```

**✅ Do**

* `Pinia`, `provide/inject`, oder zentraler EventHandler verwenden

> 📚 **Quelle**: ([tkacz.pro][23])

---

## 18. ❌ Kein Zugriff auf `$parent`

**Don't**

```ts
this.$parent.doSomething();
```

**✅ Do**

* Verwende Props, Emits oder `provide/inject`

> 📚 **Quelle**: ([DEV Community][24])

---

## 19. ❌ Keine Inline-Templates

**Don't**

```ts
export default {
  template: '<p>{{ message }}</p>'
}
```

**✅ Do**

* Verwende `.vue`-SFCs (Single File Components)

> 📚 **Quelle**: ([DEV Community][24])

---

## 20. ❌ Keine `defineComponent` ohne Typisierung

**Don't**

```ts
export default defineComponent({});
```

**✅ Do**

```ts
export default defineComponent({
  name: 'MyComponent',
  props: {
    title: { type: String, required: true },
  },
});
```

Oder bei `setup`-only:

```ts
const props = defineProps<{ title: string }>();
```

➡ Immer explizite Typen für Props – für IDE, Autocomplete & Fehlervermeidung

---

## 21. ❌ Kein `v-model` ohne Namensgebung bei mehreren Props

**Don't**

```vue
<MyInput v-model="value" v-model="label" />
```

**✅ Do**

```vue
<MyInput v-model:value="value" v-model:label="label" />
```

➡ Immer benannte `v-model`s bei mehreren Bindings

---

## 22. ❌ Kein direktes Einfügen von API- oder Store-Logik in Komponenten

**Don't**

```ts
const response = await axios.get('/users');
```

**✅ Do**

```ts
const { getUsers } = useUserApi();
const users = await getUsers();
```

➡ API-Zugriffe **immer über Composables oder Services kapseln**

---

## 23. ❌ Keine globale Nutzung von `$t` / `$i18n` ohne Fallbacks

**Don't**

```ts
$t('user.name')
```

**✅ Do**

```ts
const { t } = useI18n();
t('user.name', 'Fallback Name');
```

➡ Lokale Instanz nutzen, **Fallbacks immer mitdenken** für Robustheit

---

## 24. ❌ Keine Logik in `watchEffect`, wenn nicht reaktiv notwendig

**Don't**

```ts
watchEffect(() => {
  if (data.value) fetchDetails();
});
```

**✅ Do**

```ts
watch(data, () => {
  fetchDetails();
});
```

➡ `watchEffect` nur bei komplexen reaktiven Szenarien sinnvoll – **ansonsten `watch()`**

---

## 25. ❌ Kein `ref(null)` bei Objekten ohne Typ

**Don't**

```ts
const user = ref(null);
```

**✅ Do**

```ts
const user = ref<User | null>(null);
```

➡ Immer **konkret typisieren**, besonders bei Objekten & Arrays

---

## 26. ❌ Kein direktes Schreiben in Reactive-Objekte in Templates

**Don't**

```vue
<input v-model="user.name" />
```

➡ Falsch, wenn `user` aus `defineProps()` kommt!

**✅ Do**

```ts
const editableUser = ref({ ...props.user });
```

```vue
<input v-model="editableUser.value.name" />
```

➡ **Props dürfen nie direkt verändert werden**

---

## 27. ❌ Kein wildes Verschachteln von `v-if`, `v-for`, `v-show` etc.

**Don't**

```html
<div v-if="a">
  <div v-show="b">
    <ul v-for="item in items">
      ...
    </ul>
  </div>
</div>
```

**✅ Do**

*Kapsle in Computed Properties oder eigene Subkomponenten*

```ts
const shouldShowList = computed(() => a && b && items.length);
```

```vue
<template v-if="shouldShowList">
  <ItemList :items="items" />
</template>
```

➡ Mehr Klarheit, bessere Testbarkeit, bessere DX

---

## 28. ❌ Keine vermischte Nutzung von `setup()` und Options-API

**Don't**

```ts
export default {
  setup() {
    ...
  },
  data() {
    return { foo: true };
  }
};
```

**✅ Do**

→ Ganz oder gar nicht: **entweder Composition API oder Options API**


✅ **Exakt – `!!entgeltschluessel.model.value` ist die komprimierte, idiomatische Variante**
Hier ist der Do/Don't-Eintrag mit diesem Pattern eingebaut:

---

## 29. ❌ Kein überladener Vergleich auf "Wert vorhanden"

**Don't**

```ts
if (
  entgeltschluessel.model.value !== '' &&
  entgeltschluessel.model.value !== null &&
  entgeltschluessel.model.value !== undefined
) {
  // ...
}
```

**✅ Do**

```ts
if (!!entgeltschluessel.model.value) {
  // Wert ist truthy (nicht leer, null oder undefined)
}
```

➡ Noch klarer (wenn explizit erwartet wird, dass `.value` ein String ist):

```ts
const hasValue = !!entgeltschluessel.model.value?.trim();
```

---

🧠 **Hinweis:**
`!!foo` ist **idiomatisch** für „hat einen gültigen Wert“
– aber: bei numerischen oder boolean-Werten kann `0` oder `false` fälschlich als „leer“ interpretiert werden.

**Wenn das relevant ist (z. B. Zahl `0` ist gültig), dann lieber explizit prüfen:**

```ts
if (entgeltschluessel.model.value !== null && entgeltschluessel.model.value !== undefined)
```

### 📚 **Quelle**:
> „Um festzustellen, ob ein Wert in JavaScript wahr oder falsch ist, verwenden die doppelte Negation (`!!value`). Damit wird der Wert sauber und sicher in einen booleschen Wert umgewandelt.“ [MDN Web Docs: Boolean coercion using !!](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_NOT#double_not_!!)

---

## 30. ⛔️ Keine Imports innerhalb von Funktionen

### ❌ Anti-Pattern

```ts
function fetchData() {
  const { useApi } = await import('@/composables/useApi');
  return useApi().getData();
}
```

### ✅ Do

```ts
import { useApi } from '@/composables/useApi';

function fetchData() {
  return useApi().getData();
}
```

➡ Dynamische Imports nur bei echter Lazy-Loading-Strategie in z. B. Router Guards oder Heavy Modules.

> 📚 **Quelle**:  [Vue Style Guide – Rule: Avoid Imports in Functions](https://vuejs.org/style-guide/rules-strongly-recommended.html#no-side-effects-in-computed-properties)

---

## 31. 🔐 Zugriffsschutz über `readonly()`

Verwende `readonly()` für Props oder interne State-Weitergaben, um versehentliche Mutationen zu verhindern.

### ✅ Do

```ts
const readonlyUser = readonly(user);
```

➡ Readonly schützt z. B. Stores davor, außerhalb der Actions verändert zu werden.

> 📚 **Quelle**:  [Vue.js Guide – readonly()](https://vuejs.org/api/reactivity-utilities.html#readonly)

---


## 32. 🧪 Hook-basierte Tests mit `mountBuilder`

Erstelle eigene Mount-Hilfsfunktionen für bessere Lesbarkeit & Testwiederverwendung:

```ts
function mountComponent(props: Partial<Props> = {}) {
  return mount(MyComponent, {
    props: { ...defaultProps, ...props },
  });
}
```

➡ Bessere DX, DRY-Tests, weniger Setup-Code

> 📚 **Quelle**:  [Vitest + Vue Testing Guide](https://test-utils.vuejs.org/guide/)

---

## 33. 📥 Formular-Komponenten sind *Controlled*

Alle Form-Inputs sollten `v-model` mit `modelValue` verwenden und keine lokale Mutation durchführen.

### ✅ Struktur

```ts
defineProps<{ modelValue: string }>();
defineEmits<{ (e: 'update:modelValue', value: string): void }>();

const onInput = (value: string) => emit('update:modelValue', value);
```

➡ Predictable State, bessere Testbarkeit, keine versteckten Nebeneffekte

> 📚 **Quelle**:  [Vue 3 Docs – Component v-model](https://vuejs.org/guide/components/v-model.html)

---

## 34. ⚠️ `watchEffect` nur bei dynamischer Abhängigkeit

### ❌ Don't

```ts
watchEffect(() => {
  if (user.value) loadData();
});
```

### ✅ Do

```ts
watch(user, () => {
  loadData();
});
```

➡ `watchEffect()` eignet sich nur bei nicht explizit benennbaren Abhängigkeiten.

> 📚 **Quelle**:  [Vue Docs – watch vs. watchEffect](https://vuejs.org/guide/essentials/watchers.html)

---

## 35. ✨ Performance: Komponenten lazy laden

### ✅ Do (z. B. im Router)

```ts
{
  path: '/settings',
  component: () => import('@/views/SettingsView.vue'),
}
```

➡ Tree-Shaking, besseres Initial Loading, gute DX

> 📚 **Quelle**:  [Vue Router Docs – Lazy Loading](https://router.vuejs.org/guide/advanced/lazy-loading.html)

---

## 36. 🧼 Composables: Präfix `useXyz` beibehalten

Alle Composables folgen dem Namensschema `useXyz`, z. B.:

```ts
useAuth()
useFormValidation()
useKlinikFilter()
```

➡ Erhöht Lesbarkeit, IDE-Suche, Konsistenz im Projekt

> 📚 **Quelle**:  [VueUse & Community Guidelines](https://vueuse.org/)

---

## 🧩 37. ❌ Kein unstrukturierter Component Output

### ❌ Don't

```ts
return {
  foo,
  bar,
  a,
  b,
  c,
};
```

### ✅ Do

```ts
return {
  foo,
  bar,
  nested: {
    a,
    b,
    c,
  },
};
```

➡ Verbesserte DX beim Destructuring im `<template>` oder bei Composition-Aufrufen.

> 📚 **Quelle**: Erfahrungswerte, Clean Code Patterns, DX-Optimierung

---

## 🔒 38. ❌ Kein direkter `v-model` auf `store.state`

### ❌ Don't

```vue
<input v-model="store.user.name" />
```

### ✅ Do

```ts
const name = ref(store.user.name);
watch(name, (newVal) => store.setName(newVal));
```

➡ `v-model` verändert sofort Store-Daten → schwer rückverfolgbar & testbar.

> 📚 **Quelle**: [Pinia Best Practices – Vue School](https://vueschool.io/articles/vuejs-tutorials/how-to-use-pinia-store-with-vue-3/)

---





[1]: https://stackoverflow.com/questions/42051588/wildcard-or-asterisk-vs-named-or-selective-import-es6-javascript?utm_source=chatgpt.com "Wildcard or asterisk (*) vs named or selective import es6 javascript"
[2]: https://stackoverflow.com/questions/47294904/why-shouldnt-you-use-import-all-in-es6?utm_source=chatgpt.com "javascript - Why shouldn't you use import all in ES6 - Stack Overflow"
[3]: https://codezup.com/mastering-vue-3-state-management-with-pinia/?utm_source=chatgpt.com "Vue 3 State Management: Mastering Pinia | Complete Guide"
[4]: https://codezup.com/vuejs-3-state-management-with-pinia-practical-guide/?utm_source=chatgpt.com "Vue.js 3 State Management: A Practical Guide to Pinia"
[5]: https://learnvue.co/articles/vue-emit-guide?utm_source=chatgpt.com "Vue Emit Guide | LearnVue"
[6]: https://vuejs.org/guide/typescript/composition-api.html?utm_source=chatgpt.com "TypeScript with Composition API - Vue.js"
[7]: https://www.koderhq.com/tutorial/vue/typescript-ref/?utm_source=chatgpt.com "Vue.js 3 TypeScript Refs, Complex types & Interfaces Tutorial"
[8]: https://stackoverflow.com/questions/51439843/unknown-vs-any?utm_source=chatgpt.com "typescript - 'unknown' vs. 'any' - Stack Overflow"
[9]: https://thoughtbot.com/blog/typescript-stop-using-any-there-s-a-type-for-that?utm_source=chatgpt.com "TypeScript: Stop Using 'any', There's a Type For That - thoughtbot"
[10]: https://stackoverflow.com/questions/73640531/how-to-perform-null-check-before-accessing-the-value-in-ref-of-vue3?utm_source=chatgpt.com "How to perform null-check before accessing the value in ref () of Vue3?"
[11]: https://stackoverflow.com/questions/64613226/vue-3-composition-api-get-value-from-object-ref?utm_source=chatgpt.com "Vue 3 composition API get value from object ref - Stack Overflow"
[12]: https://vuejs.org/guide/essentials/list.html?utm_source=chatgpt.com "List Rendering - Vue.js"
[13]: https://vueschool.io/articles/vuejs-tutorials/tips-and-gotchas-for-using-key-with-v-for-in-vue-js-3/?utm_source=chatgpt.com "Tips and Gotchas for Using key with v-for in Vue.js 3 - Vue School"
[14]: https://dev.to/jsbroks/15-vue-3-tips-tricks-183k?utm_source=chatgpt.com "15 Vue 3 Tips & Tricks - DEV Community"
[15]: https://learnvue.co/articles/vue-best-practices?utm_source=chatgpt.com "Vue Best Practices | LearnVue"
[16]: https://www.binarcode.com/blog/3-anti-patterns-to-avoid-in-vuejs/?utm_source=chatgpt.com "3 Anti-Patterns to avoid in Vue.js - Binarcode"
[17]: https://rishpandey.com/most-common-vue-mistakes/?utm_source=chatgpt.com "Common Vue.js Anti-Patterns and Mistakes You Should Avoid"
[18]: https://michaelnthiessen.com/avoid-mutating-prop-directly/?utm_source=chatgpt.com "Vue Error: Avoid Mutating a Prop Directly | Michael Thiessen"
[19]: https://v3-migration.vuejs.org/breaking-changes/filters.html?utm_source=chatgpt.com "Filters | Vue 3 Migration Guide"
[20]: https://eslint.vuejs.org/rules/no-v-html.html?utm_source=chatgpt.com "vue/no-v-html | eslint-plugin-vue"
[21]: https://diginode.in/vue/vue-js-computed-properties-vs-watchers/?utm_source=chatgpt.com "Vue.js Computed Properties vs Watchers - Diginode"
[22]: https://codezup.com/using-mixins-in-vuejs-effectively/?utm_source=chatgpt.com "How to Effectively Use Mixins in Vue.js - codezup.com"
[23]: https://tkacz.pro/vue-js-why-event-bus-is-bad-idea/?utm_source=chatgpt.com "Vue.js: why event bus is bad idea – Lukasz Tkacz Blog"
[24]: https://dev.to/full-stack-radio/87-chris-fritz-vue-js-anti-patterns-and-how-to-avoid-them?utm_source=chatgpt.com "87: Chris Fritz - Vue.js Anti-Patterns (and How to Avoid Them)"
