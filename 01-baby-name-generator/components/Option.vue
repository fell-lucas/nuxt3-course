<script setup lang="ts">
import { Gender, Length, Popularity } from "~~/data";

interface Props {
  option: {
    title: string;
    category: string;
    buttons: Gender[] | Popularity[] | Length[];
  };
  state: {
    gender: Gender;
    popularity: Popularity;
    length: Length;
  };
}

const { option, state } = defineProps<Props>();

const computeButtonClasses = (value, index: number) => {
  const classNames = [];
  if (state[option.category] === value) {
    classNames.push("option-active");
  }
  if (index === 0) classNames.push("option-left");
  if (index === option.buttons.length - 1) classNames.push("option-right");
  return classNames.join(" ");
};
</script>

<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>
    <button
      v-for="(value, index) in option.buttons"
      :key="value"
      class="option"
      :class="computeButtonClasses(value, index)"
      @click="state[option.category] = value"
    >
      {{ value }}
    </button>
  </div>
</template>

<style scoped>
.option-container {
  margin-bottom: 2rem;
}

.option {
  background-color: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}

.option-left {
  border-radius: 1rem 0 0 1rem;
}

.option-right {
  border-radius: 0 1rem 1rem 0;
}

.option-active {
  background-color: rgb(249, 87, 89);
  color: white;
}
</style>
