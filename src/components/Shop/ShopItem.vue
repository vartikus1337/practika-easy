<script setup>
import { inject, ref } from 'vue';
import { srcPngHelper } from '@/components/utils';

import IconPlatform from './IconPlatform.vue';

defineProps(['nameGame', 'money', 'imgSrc', 'platforms', 'id']);

const selected = inject('selectedPlatforms');
const data = inject('data');

const isActive = ref(false);
</script>

<template>
  <div class="game" v-show="selected && platforms.includes(selected)">
    <img
      class="game__img"
      @mouseover="isActive = !isActive"
      :src="srcPngHelper(imgSrc)"
      alt="Фото игры"
    />
    <div :class="['game__about', { active: isActive }]" @mouseleave="isActive = !isActive">
      <h1>{{ nameGame }}</h1>
      <h2>{{ money }}₽</h2>
      <div class="game__about-btns">
        <!-- <button class="game__about-btn">Подробнее</button> -->
        <button
          class="game__about-btn-buy"
          v-if="data.user.value.isLogged"
          @click="data.selectGames.value.push(id)"
        >
          Купить
        </button>
      </div>
    </div>
    <div class="platforms">
      <IconPlatform v-for="platform in platforms" :platform="platform" :key="platform" />
    </div>
  </div>
</template>

<style scoped>
.game {
  display: flex;
  position: relative;
}

.game__img {
  height: 300px;
  width: min-content;
  cursor: pointer;
}

.game__about {
  display: none;
}

.game__about h1 {
  font-weight: 700;
  font-size: 32px;
  line-height: 38px;
  text-align: center;
  color: #ffffff;
}

.game__about h2 {
  font-weight: 700;
  font-size: 20px;
  line-height: 23px;
  text-align: center;
  color: #ffffff;
}

.game__about.active {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 30px;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
}

.game__about-btns {
  display: flex;
  gap: 20px;
}

.game__about-btn-buy {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  width: fit-content;
  background: #9bf00b;
  font-weight: 700;
  font-size: 16px;
  line-height: 19px;
  color: #054b16;
}

.game__about-btn {
  display: flex;
  width: 100%;
  justify-content: center;
  align-items: center;
  padding: 10px;
  gap: 10px;
  margin: 0 auto;
  background: #9bf00b;
  border-radius: 50px;
  font-weight: 700;
  color: #054b16;
}

.platforms {
  display: flex;
  align-items: center;
  gap: 5px;
  position: absolute;
  width: 100%;
  height: 40px;
  left: 0px;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
}

.game__about.active + .platforms {
  display: none;
}

.platforms > * {
  width: 40px;
  height: 40px;
}
</style>
