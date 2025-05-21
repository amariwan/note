## ✅ Erweiterte Struktur-Hierarchie: Best Practices + Tipps

```ts
<script setup lang="ts">
/* ───────────── 1. 📦 Imports ───────────── */
// 💡 Sortierung: Vue Core → Libs → Projekt → Relativ
import { useI18n } from 'vue-i18n';
import { useRoute, useRouter } from 'vue-router';
import { useToast } from 'vue-toastification';


import { formatDate } from '@/utils/date';
import { useFormValidation } from '@/composables';
import {SaveButton} from '@/components';

/* ───────────── 2. 🧱 Typen ───────────── */
// 💡 Immer externe Typen importieren, wenn möglich
interface Props {
  userId: string;
}
type FormData = Record<string, string | number | boolean>;

/* ───────────── 3. 🎯 Props & Emits ───────────── */
const props = defineProps<Props>();
const emit = defineEmits<{
  (e: 'update', value: string): void;
  (e: 'cancel'): void;
}>();

/* ───────────── 4. 🌍 Global Context ───────────── */
// 💡 Nur was im Template gebraucht wird, exportieren!
const { t } = useI18n();
const router = useRouter();
const route = useRoute();
const toast = useToast();

/* ───────────── 5. 🧪 Lokaler Zustand ───────────── */
const isLoading = ref(false);
const formData = ref<FormData>({});
const isDirty = ref(false);

/* ───────────── 6. 🧮 Computed ───────────── */
const isValid = computed(() => !!formData.value?.name);

/* ───────────── 7. 🧠 Methoden ───────────── */
// 💡 Methoden klar trennen: I/O, Formatierung, Interaktion
function handleSubmit(): void {
  if (!isValid.value) return toast.error(t('error.form.invalid'));
  emit('update', JSON.stringify(formData.value));
}

function resetForm(): void {
  formData.value = {};
  isDirty.value = false;
  emit('cancel');
}

/* ───────────── 8. 🧭 Watcher ───────────── */
// 💡 Watch separat von Lifecycle
watch(formData, () => {
  isDirty.value = true;
}, { deep: true });

/* ───────────── 9. 🚀 Lifecycle ───────────── */
onMounted(() => {
  fetchInitialData();
});

async function fetchInitialData() {

}

/* ───────────── 10. 🔓 Expose (wenn nötig) ───────────── */
defineExpose({ resetForm });
</script>
```

---

## 📚 Weiterführende Ressourcen

| Thema                           | Quelle                                                                                                                         |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `<script setup>` Guide          | [https://vuejs.org/api/sfc-script-setup.html](https://vuejs.org/api/sfc-script-setup.html)                                     |
| Vue Composition Style Guide     | [https://vuejs.org/style-guide/rules-strongly-recommended.html](https://vuejs.org/style-guide/rules-strongly-recommended.html) |
| TypeScript + Vue Best Practices | [https://vuejs.org/guide/typescript/overview.html](https://vuejs.org/guide/typescript/overview.html)                           |
| Composable Conventions          | [https://vueuse.org/](https://vueuse.org/)                                                                                     |
| Testing Best Practices          | [https://test-utils.vuejs.org/guide/](https://test-utils.vuejs.org/guide/)                                                     |
