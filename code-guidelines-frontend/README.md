# 🧭 Architektur- und Code-Guidelines für Vue 3

## 1. Architektur-Leitlinie: Trennung von App & Komponenten

### 🔹 App-Schicht (Container-Logik)

Nur die **App-Container-Komponente** (View, Page, App) kommuniziert mit:

* Pinia-Stores
* APIs
* globalem State

**Aufgaben:**

* Daten laden & speichern über Stores (`fetch`, `save`, etc.)
* Verwalten von `loading`/`error`-States
* Weitergabe der States an Child-Komponenten via Props
* Übergibt Daten an UI-Komponenten

**Beispielstruktur:**

```ts
<App>
  ├──<KlinikView>
  |  ├── 📥 erhält Daten & Status aus Store
  |  └── 📤 reicht Props & Events an Komponenten weiter
  └── <...>
```

---

### 🔹 Komponenten-Schicht (Presentational)

**Prinzip: Dumb Components**

* Nur Props erhalten
* Emitten Events
* Keine Store-/API-Zugriffe
* Keine Business-Logik

**Beispiel:**

```vue
<template>
  <SaveButton :disabled="!isValid" @click="onSave" />
</template>

<script setup lang="ts">
const props = defineProps<{ isValid: boolean }>();
const emit = defineEmits<{ (e: 'save'): void }>();

function onSave(): void {
  emit('save');
}
</script>
```

---

## 2. 🚫 Keine Logik in Templates

### ❌ Anti-Pattern:

```vue
<v-col
  v-if="!props.invisibleFields?.includes('zimmerartSonstige') && zimmerart.model.value?.name === 'Sonstige'"
  cols="4"
>
  <v-textarea
    v-model="zimmerartSonstige.model.value"
    :error-messages="(...) ? '' : 'Fehler'"
  />
</v-col>
```

**Probleme:**

* Schwer testbar
* Unleserlich
* Kein Separation of Concerns

### ✅ Besser: Script auslagern

```vue
<template>
  <v-col v-if="zimmerartSonstigeInput.shouldShow" cols="4">
    <v-textarea
      v-model="zimmerartSonstigeInput.model"
      :error-messages="zimmerartSonstigeInput.error"
    />
  </v-col>
</template>

<script setup lang="ts">
const zimmerartSonstigeInput = {
  model: zimmerartSonstige.model.value,
  shouldShow: computed(() => ...),
  error: computed(() => ...),
};
</script>
```

---

## 3. 🧼 Clean Templates Prinzip

**Logik gehört in:**

* `computed`
* `methods`
* ggf. `composables`

---

## 4. ✅ Vue 3 Reaktivität im Überblick

| Art             | Typ                          | Use Case                                      |
| --------------- | ---------------------------- | --------------------------------------------- |
| `ref<T>()`      | Reaktiver Wrapper (Primitiv) | `const count = ref<number>(0)`                |
| `reactive()`    | Reaktives Objekt             | `const user = reactive({ name: '', age: 0 })` |
| `computed<T>()` | Abgeleiteter Zustand         | `const isValid = computed(() => ...)`         |
| Variable        | Nicht-reaktiv                | `let temp = 0`                                |

> 💡 Immer explizit typisieren!

---

## 5. 📏 Regeln & Best Practices

### 🔸 Import-Regeln

* Nur `@/` verwenden
* Kein `../../`
* Keine Wildcard-Imports

### 🔸 Komponentenstruktur

* `<template>` immer vor `<script>`
* Keine Event-Handler inline im Template

```ts
function onClick() { emit('save') }
```

```html
<button @click="onClick">Speichern</button>
```

### 🔸 Typisierung

* Alles typisieren
* Booleans benennen: `isXyz`, `hasXyz`
* Funktionen mit Rückgabetyp:

```ts
function loadUser(): Promise<User> { ... }
```

---

## 6. 🧪 Feature-Toggle & Refactoring

* Nutze Feature-Flags: `const isFeatureXEnabled = true`
* Neue Logik → Composable
* Alte Logik fallbackfähig halten
* Kein Hard-Cutoff

---

## 7. ✅ Teststrategie

* User Story basiert
* Isolierte Komponenten-Tests
* Unit-Tests für Businesslogik
* Integrationstests
* E2E mit Playwright

---

## 8. 🎯 Merkmale guter Komponenten

* Klare Trennung UI vs. Logik
* Props in, Emits out
* Keine externen Zugriffe
* Strukturiert: Imports → Props → Emits → Logic
* Selbstbeschreibend & typisiert

---

## 9. ⚖️ Unterschied `??` vs `||`

| Operator | Bedeutung          | Rückgabekriterium                            |            |                                    |
| -------- | ------------------ | -------------------------------------------- | ---------- | ---------------------------------- |
| \`       |                    | \`                                           | Logical OR | Gibt rechten Wert zurück bei falsy |
| `??`     | Nullish Coalescing | Gibt rechten Wert nur bei `null`/`undefined` |            |                                    |

**Beispiele:**

```ts
'' || 'fallback'  // → 'fallback'
'' ?? 'fallback'  // → ''
```

### Empfehlung:

| Für               | Verwende |                     |    |
| ----------------- | -------- | ------------------- | -- |
| Props & `.value`  | `??`     |                     |    |
| Anzeige-Fallbacks | \`       |                     | \` |
| Niemals \`        |          | `bei Zahlen wie`0\` |    |

---

## 10. ✍️ Code Guidelines erzwingen

* `eslint` + `prettier` für Style und Struktur
* Review-Regeln: PRs mit Typen & Tests

---

## 11. 📖 Self-Documenting Code

* Gute Bezeichner (was + warum)
* Keine Kommentare für triviale Dinge
* Methoden zerlegen und wiederverwenden

---

## 12. 🛡 Events: Keine `.value` direkt im Template

**Nicht:**

```ts
onClick={() => doSomething(thing.value)}
```

**Sondern:**

```ts
function onClick() {
  doSomething(thing.value)
}
```

---

## 13. 🧱 Komponentenkomposition: Strikte Verantwortungstrennung

**🔹 Regel:** *1 Komponente = 1 Aufgabe = 1 Verantwortung*

### ✅ Komposition statt Vererbung

**Do**

```vue
<!-- Dumb component -->
<FormField :label="t('user.name')">
  <input v-model="form.name" />
</FormField>
```

➡ Komplexe Form-Layouts mit Slots, nicht verschachtelter Logik

---

## 14. 🔄 Controlled vs. Uncontrolled Components

Verwende `v-model` **nur wenn** die Komponente kontrolliert wird. Sonst: explizite `modelValue` + `update:modelValue`

### ✅ Do

```ts
defineProps<{ modelValue: string }>();
defineEmits<{ (e: 'update:modelValue', value: string): void }>();
```

### ❌ Don't

```vue
<input :value="modelValue" @input="modelValue = $event.target.value" /> ❌
```

➡ Das **mutiert Prop direkt**, was zu Fehlern führt

---

## 15. 🧪 Testbare Architektur durch saubere Trennung

### ✅ Do

* Businesslogik in `composables/` auslagern
* Echte Tests schreiben für:

  * Form-Validation
  * Computed Properties
  * API-Zugriffe (mocked)
  * Event-Kaskaden

---

## 16. 🧩 Stores nach Feature, nicht nach Entity

### ❌ Anti-Pattern

```ts
// stores/user.ts
export const useUserStore = defineStore(...);
```

### ✅ Feature-orientiert

```ts
// stores/userManagement.ts
export const useUserManagementStore = defineStore(...);
```

➡ Klarer Bezug zum UI-Kontext → bessere Wartbarkeit bei wachsendem System

---

## 17. 🧭 i18n Best Practices

* Immer mit **Keys arbeiten**, nie mit rohen Strings
* **Fallbacks definieren**
* Struktur:

```json
{
  "user": {
    "name": "Name",
    "email": "E-Mail"
  }
}
```

* Keys in Gruppen: `user.name`, `form.submit`, `error.validation.emailRequired`

---

## 18. 🧪 `Zod` + `Vee-Validate`: Validierung auslagern

### ✅ Struktur:

```ts
const schema = z.object({
  name: z.string().min(1),
  age: z.number().min(18),
});
```

```ts
const { handleSubmit } = useForm({ validationSchema: toTypedSchema(schema) });
```

➡ Schema = Single Source of Truth → validierbar, testbar, typisiert

---

## 19. 🧼 Slot-Nutzung strukturieren

### ✅ Benannte Slots mit Struktur

```vue
<BaseCard>
  <template #header>...</template>
  <template #default>...</template>
  <template #footer>...</template>
</BaseCard>
```

➡ Klar, wartbar, leicht testbar

---

## 20. 🚥 Error- & Loading-Handling zentralisieren

### ✅ Statusmodell für jede API-Operation

```ts
type AsyncState<T> = {
  loading: boolean;
  error: string | null;
  data: T | null;
};
```

➡ Perfekte UX + testbarer Zustand + klarer Flow

---

## 📚 Quellen & weiterführende Best Practices

* [Vue Style Guide (Official)](https://vuejs.org/guide/reusability/style-guide.html)
* [Vue Use Composition Best Practices](https://vueuse.org/guide/)
* [Zod + VeeValidate Integration](https://vee-validate.logaretm.com/v4/guide/composition-api/zod/)
* [Playwright Testing Guide](https://playwright.dev/docs/test-intro)
