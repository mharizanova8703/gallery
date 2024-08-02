<template>
  <div class="photo">
    <img :src="photo.url" @click="removePhoto" />
    <button class="favorite-button" @click="toggleFavorite" :class="{'active': photo.isFavorite}">
      <img 
        :src="photo.isFavorite ? 'https://bm-projects-public.s3.amazonaws.com/loyl19001/production/site_55/images/star.png' : 'https://icon2.cleanpng.com/20180330/rdq/avc213q7u.webp'"
        class="star-img">
    </button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  photo: Object,
  index: Number
});

const emit = defineEmits(['remove', 'toggle']);

const removePhoto = () => {
  emit('remove', props.index);
};

const toggleFavorite = () => {
  emit('toggle', props.photo);
};
</script>

<style scoped>
.photo {
  background-color: white;
  position: relative;
  border: 1px solid #ccc;
}

.photo img {
  width: 100%;
  display: block;
}

.favorite-button {
  background: none;
  border: none;
  font-size: 24px;
  position: absolute;
  bottom: 5px;
  right: -18px;
  cursor: pointer;
}

.favorite-button.active {
  color: gold;
}

.favorite-button .star-img {
  width: 20px;
  height: 20px;
}
</style>
