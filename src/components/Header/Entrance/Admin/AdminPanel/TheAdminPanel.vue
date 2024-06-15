<script setup>
import axios from 'axios';
import { inject, onMounted, reactive } from 'vue';

import AddUser from './Add/TheAddUser.vue';
import AddNew from './Add/TheAddNew.vue';
import AddComment from './Add/TheAddComment.vue';
import AddGame from './Add/TheAddGame.vue';
import UploadImg from './Add/TheUploadImg.vue';

import ChangeUsers from './Change/TheChangeUsers.vue';
import ChangeNews from './Change/TheChangeNews.vue';
import ChangeComments from './Change/TheChangeComments.vue';
import ChangeGames from './Change/TheChangeGames.vue';
import ChangeImgs from './Change/TheChangeImgs.vue';

const data = inject('dataAdmin');
const dataUser = inject('data');
const section = inject('section');
const subSection = inject('subSection');

onMounted(async () => {
  if (!Object.keys(data).length) {
    const user = dataUser.user.value;
    try {
      const response = await axios.post('http://localhost:3000/admin_data', {
        username: user.name,
        password: user.passAdmin
      });
      ['users', 'news', 'games', 'comments'].forEach(
        (el) => (data[el] = reactive(response.data[el]))
      );
    } catch (error) {
      console.error(error);
    }
  }
});
</script>

<template>
  <div v-if="section == 'Добавить'" class="add">
    <AddUser v-if="section == 'Добавить' && subSection == 'Users'" />
    <AddNew v-if="section == 'Добавить' && subSection == 'News'" />
    <AddComment v-if="section == 'Добавить' && subSection == 'Comments'" />
    <AddGame v-if="section == 'Добавить' && subSection == 'Games'" />
    <UploadImg v-if="section == 'Добавить' && subSection == 'Img'" />
  </div>
  <div v-if="section == 'Изменить'" class="change">
    <h1 class="warning">Изменения происходят реактивно!</h1>
    <ChangeUsers v-if="section == 'Изменить' && subSection == 'Users'" />
    <ChangeNews v-if="section == 'Изменить' && subSection == 'News'" />
    <ChangeComments v-if="section == 'Изменить' && subSection == 'Comments'" />
    <ChangeGames v-if="section == 'Изменить' && subSection == 'Games'" />
    <ChangeImgs v-if="section == 'Изменить' && subSection == 'Img'" />
  </div>
</template>

<style scoped>
.change {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
