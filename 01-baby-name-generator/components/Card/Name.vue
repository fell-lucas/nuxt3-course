<script setup lang="ts">
interface Props {
  name: string;
}

defineProps<Props>();

const emit = defineEmits(["remove"]);
</script>

<template>
  <div class="card">
    {{ name }}
    <p @click="emit('remove')">x</p>
  </div>
</template>

<style scoped>
.card p {
  position: absolute;
  top: -28%;
  left: 94%;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.5);
}

.card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}
</style>
