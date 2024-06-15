<script setup>
import { inject } from 'vue';

const data = inject('dataAdmin');
</script>

<template>
  <div class="change-comments">
    <ul v-if="Object.keys(data.comments).length">
      <li>
        <h2 v-for="key in Object.keys(data.comments[0])" :key="key">{{ key }}</h2>
      </li>
      <li v-for="(index, comment) in data.comments" :key="index">
        <input type="text" v-model="comment.name" placeholder="username" />
        <input type="text" v-model="comment.email" placeholder="email" />
        <input type="email" v-model="comment.text" placeholder="text" />
      </li>
    </ul>
    <h1 v-else class="warning">Пустой</h1>
  </div>
</template>
