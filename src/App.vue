<template>
  <h1>Users Fetch</h1>
  <input
    type="text"
    id="input"
    v-model="userId"
    v-on:change="getData"
    placeholder="Search user by id"
  />
  <div v-if="apiData" class="cards-container">
    <div v-for="element in apiData" :key="element.id">
      <Card
        :id="element.id"
        :title="element.title"
        :name="`${element.firstName} ${element.lastName}`"
        :picture="element.picture"
        :email="element.email"
      />
    </div>
  </div>
  <div v-if="!apiData">Loading...</div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import Card from "./components/Card.vue";

interface User {
  id: string;
  title: string;
  firstName: string;
  lastName: string;
  picture: string;
  email: string | undefined;
}

const apiData = ref<User[]>([]);
const userId = ref<String>("");

const setValues = (data: any, isOneUserOnly: boolean) => {
  console.log(data);
  if (isOneUserOnly) {
    apiData.value = [
      {
        id: data.id,
        title: data.title,
        firstName: data.firstName,
        lastName: data.lastName,
        picture: data.picture,
        email: data.email,
      },
    ];
  } else {
    apiData.value = [...data.data];
  }
};

const getData = async () => {
  const url = userId.value
    ? "https://dummyapi.io/data/v1/user/" + userId.value
    : "https://dummyapi.io/data/v1/user?limit=10";
  const options: Object = {
    headers: {
      "app-id": "646e8690663cdd387105b5fc",
    },
  };

  fetch(url, options)
    .then((response) => response.json())
    .then((data) => setValues(data, Boolean(userId.value)));
};

onMounted(() => {
  getData();
});
</script>

<style>
.cards-container {
  margin-top: 6rem;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  background-color: #3b3b3b;
  border-radius: 1rem;
}
</style>
