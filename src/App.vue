<script setup>
  import quizesData from './data/quizes.json';
  import { ref, watch } from 'vue';
  import Card from './components/Card.vue';

  const quizes = ref(quizesData),
        search = ref('');

  watch(search, () => {
    quizes.value = quizesData.filter(quize => {
      return quize.name.toLowerCase().includes(search.value)
    });
  });
</script>

<template>
  <div class="container">
    <header>
      <h1>Quizes</h1>
      <input v-model.trim.toLowerCase="search" type="text" placeholder="Search...">
    </header>

    <div class="options-container">
      
      <!-- <div v-for="quiz in quizes" :key="quiz.id" class="card">
        <img :src="quiz.img" alt="">
        <div class="card-text">
          <h2>{{ quiz.name }}</h2>
          <p>{{ quiz.questions.length }} questions</p>
        </div>
      </div> -->

      <Card :quizes="quizes"/>

    </div>
  </div>
</template>

<style scoped>
  .container {
    max-width: 1000px;
    margin: 0 auto;
  }

  header {
    margin: 30px 0 10px 0;
    display: flex;
    align-items: center;
  }

  header h1 {
    font-weight: bold;
    margin-right: 30px;
  }

  header input {
    border: none;
    background-color: rgba(128, 128, 128, 0.1);
    padding: 10px;
    border-radius: 5px;
  }

  .options-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
  }
</style>