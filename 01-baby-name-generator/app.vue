<script setup lang="ts">
import { Gender, Popularity, Length, names } from "./data";

interface OptionsState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const options: OptionsState = reactive({
  gender: Gender.GIRL,
  popularity: Popularity.TRENDY,
  length: Length.ALL,
});

const selectedNames = ref<string[]>([]);

const computeSelectedNames = () => {
  const filteredNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    });
  selectedNames.value = filteredNames.map((name) => name.name);
};

const optionsArray = [
  {
    title: "1) Choose a gender",
    category: "gender",
    buttons: [Gender.BOY, Gender.GIRL, Gender.UNISEX],
  },
  {
    title: "2) Choose a popularity",
    category: "popularity",
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3) Choose a length",
    category: "length",
    buttons: [Length.SHORT, Length.ALL, Length.LONG],
  },
];

const removeName = (index: number) => {
  const filteredNames = [...selectedNames.value];
  filteredNames.splice(index, 1);
  selectedNames.value = filteredNames;
};
</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click "Find Names"</p>
    <div class="options-container">
      <Option
        v-for="option in optionsArray"
        :key="option.title"
        :option="option"
        :state="options"
      />
      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>
    <div class="cards-container">
      <CardName
        v-for="(name, index) in selectedNames"
        :key="name"
        :name="name"
        @remove="() => removeName(index)"
      />
    </div>
  </div>
</template>

<style scoped>
.cards-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

h1 {
  font-size: 3em;
}

.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}

.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}
</style>
