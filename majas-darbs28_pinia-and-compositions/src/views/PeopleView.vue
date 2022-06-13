<template>
  <div>
    <form @submit.prevent="search(name)">
      <input v-model="name" placeholder="Enter name" type="text" />
      <button>Search</button>
    </form>
  </div>
  <main>
    <div v-if="loading">Loading...</div>
    <div v-else v-for="person in people" :key="person.name">
      <div>
        <h2>Name: {{ person.name }}</h2>
        <div>Birth year: {{ person.birth_year }}</div>
        <div>Eye color: {{ person.eye_color }}</div>
        <div>Hair color: {{ person.hair_color }}</div>
        <div>Gender: {{ person.gender }}</div>
        <div>Mass: {{ person.mass }}</div>
        <div>Skin color: {{ person.skin_color }}</div>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { usePeopleStore } from "@/stores/people";
import { mapActions, mapState, storeToRefs } from "pinia";
import { onMounted, computed } from "vue";
const { loading } = storeToRefs(usePeopleStore());
const name = "";
const people = computed(() => {
  return usePeopleStore().getPeople;
});
const search = (name: string) => {
  return usePeopleStore().fetchPeopleByName(name);
};
onMounted(() => {
  usePeopleStore().fetchPeople();
});
mapState(usePeopleStore, ["people"]);
mapActions(usePeopleStore, ["fetchPeople", "fetchPeopleByName"]);
</script>
