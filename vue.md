Vue.js bietet eine breite Palette von Funktionen und Optionen, die Entwicklern Flexibilität und Effizienz bieten. Hier ist eine strukturierte Übersicht über die wichtigsten Listen von **Funktionen** und **Optionen** in Vue.js:

---

## 1️⃣ **Options API**
Die Options API ist die traditionelle Methode zur Definition von Komponenten.

### **Globale Optionen**
- **el**: Ziel-Element.
- **data**: Zustandsdaten der Komponente.
- **methods**: Methoden zur Verarbeitung von Daten.
- **computed**: Berechnete Eigenschaften.
- **watch**: Beobachter für reaktive Daten.
- **template**: HTML-Template der Komponente.
- **components**: Lokale Komponentenregistrierung.
- **props**: Eigenschaften, die von der Elternkomponente übergeben werden.
- **directives**: Lokale Direktivenregistrierung.
- **filters**: Globale und lokale Filter.
- **mixins**: Hinzufügen von geteilten Funktionen.
- **emits**: Ereignisse, die von der Komponente ausgelöst werden.
- **inheritAttrs**: Ob Standardattribute geerbt werden.

---

## 2️⃣ **Composition API**
Diese API bietet eine flexiblere Methode, um logikzentrierte und wiederverwendbare Code-Module zu schreiben.

### **Hauptmethoden**
- **reactive()**: Erstellt einen reaktiven Zustand.
- **ref()**: Erstellt einen reaktiven Referenzwert.
- **computed()**: Berechnete Werte basierend auf reaktiven Daten.
- **watch()**: Beobachtet reaktive Daten oder Änderungen.
- **watchEffect()**: Führt Effekte bei Änderungen aus.
- **onMounted()**: Lifecycle-Hook nach dem Mounting.
- **onUnmounted()**: Lifecycle-Hook nach dem Unmounting.
- **onUpdated()**: Nach einem DOM-Update.
- **provide()** und **inject()**: Abhängigkeitsinjektion zwischen Eltern- und Kind-Komponenten.

---

## 3️⃣ **Directives**
### **Globale Direktiven**
- `v-bind`: Bindet Attribute oder Eigenschaften.
- `v-model`: Zwei-Wege-Datenbindung.
- `v-for`: Iteration über Listen oder Objekte.
- `v-if`, `v-else-if`, `v-else`: Bedingtes Rendering.
- `v-show`: Zeigt oder verbirgt Elemente.
- `v-on`: Fügt Ereignis-Listener hinzu.
- `v-slot`: Slot-Inhalt für benutzerdefinierte Inhalte.
- `v-html`: Fügt HTML-Inhalte ein.
- `v-text`: Fügt Textinhalte ein.

---

## 4️⃣ **Lifecycle Hooks**
- **beforeCreate()**: Bevor die Instanz erstellt wird.
- **created()**: Direkt nach der Erstellung.
- **beforeMount()**: Bevor das DOM gemountet wird.
- **mounted()**: Direkt nach dem Mounten.
- **beforeUpdate()**: Bevor die Daten aktualisiert werden.
- **updated()**: Nach der Aktualisierung.
- **beforeDestroy()** (oder **beforeUnmount()**): Vor dem Zerstören.
- **destroyed()** (oder **unmounted()**): Nach dem Zerstören.

---

## 5️⃣ **Globale API**
### **Vue 3 Features**
- **createApp()**: Erstellt eine Vue-App.
- **h()**: Funktion zum Erstellen von virtuellen DOM-Knoten.
- **defineComponent()**: Definiert eine neue Komponente.
- **nextTick()**: Führt einen Codeblock beim nächsten DOM-Update aus.
- **useRouter()**, **useStore()**: Router- und Store-Integrationen.

---

## 6️⃣ **Tools und Erweiterungen**
- **Vue Router**: Für SPA-Routing.
- **Vuex (oder Pinia)**: Für State Management.
- **Vue DevTools**: Debugging und Performance-Analyse.
- **Vite**: Entwicklungsserver und Bundler.

---

## 7️⃣ **Sonstiges**
- **Transition**: Animationsunterstützung für DOM-Elemente.
- **SSR (Server-Side Rendering)**: Für SEO und schnelle Ladezeiten.
- **Custom Directives**: Eigene Direktiven erstellen.
- **Plugins**: Globale Funktionen hinzufügen.

---

Falls du für eine bestimmte Funktion oder Option ein Beispiel benötigst, lass es mich wissen! 🔨🤖🔧
