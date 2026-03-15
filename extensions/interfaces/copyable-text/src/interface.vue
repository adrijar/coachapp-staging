<template>
  <div>
    <v-textarea
      :model-value="value"
      @update:model-value="val => $emit('input', val)"
      auto-grow
      rows="6"
    />

    <v-button small @click="copyText">
      <v-icon name="content_copy" left />
      Copiar
    </v-button>

    <span v-if="copied" style="margin-left:10px;">✅ Copiado</span>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  value: String
});

const copied = ref(false);

async function copyText() {
  await navigator.clipboard.writeText(props.value || '');
  copied.value = true;
  setTimeout(() => copied.value = false, 1500);
}
</script>