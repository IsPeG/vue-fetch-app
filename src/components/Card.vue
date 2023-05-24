<script setup lang="ts">
const props = defineProps({
  id: String,
  title: String,
  name: String,
  picture: String,
  email: String,
});
</script>

<template>
  <div class="card" :key="props.id">
    <img :src="props.picture" />
    <div class="card_text">
      <h2>{{ props.name }}</h2>
      <p>{{ props.email }}</p>
      <p style="color: #a1a1a1">{{ props.id }}</p>
    </div>
  </div>
</template>

<style scoped>
.card {
  display: flex;
  padding: 1rem;
  background-color: #888;
  margin: 1rem;
  border-radius: 1rem;
  width: 20rem;
}

.card img {
  border-radius: 50%;
  width: 5rem;
  height: 5rem;
  margin-right: 1rem;
}

.card_text {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
}
</style>
