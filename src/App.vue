<template>
    <div id="app">
      <!-- Form for Adding Photos -->
      <form @submit.prevent="addPhoto">
        <input placeholder="Enter image URL" v-model="newPhotoUrl" />
        <button type="submit">Add Photo</button>
      </form>
  
      <!-- Conditional Rendering -->
      <p class="no-photos" v-if="photos.length === 0">No photos added yet. Add some!</p>
  
      <div class="gallery" v-else>
        <!-- List Rendering using PhotoItem Component -->
        <PhotoItem 
          v-for="(photo, index) in photos" 
          :key="photo.id" 
          :photo="photo" 
          :index="index" 
          @remove="removePhoto" 
          @toggle="toggleFavorite" 
        />
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import PhotoItem from './components/PhotoItem.vue';
  
  const photos = ref([
    {
      id: 1,
      url: 'https://bm-projects-public.s3.amazonaws.com/loyl19001/production/site_55/images/hat.png',
      isFavorite: false,
    },
    {
      id: 2,
      url: 'https://bm-projects-public.s3.amazonaws.com/loyl19001/production/site_55/images/shirt.png',
      isFavorite: false,
    },
    {
      id: 3,
      url: 'https://bm-projects-public.s3.amazonaws.com/loyl19001/production/site_55/images/huddy.png',
      isFavorite: false,
    }
  ]);
  
  const newPhotoUrl = ref('');
  
  const addPhoto = () => {
    const photo = {
      id: photos.value.length + 1,
      url: newPhotoUrl.value,
      isFavorite: false,
    };
    if (newPhotoUrl.value !== '') {
      photos.value.push(photo);
      newPhotoUrl.value = '';
    }
  };
  
  const toggleFavorite = (photo) => {
    photo.isFavorite = !photo.isFavorite;
    console.log(`Photo ID: ${photo.id}, isFavorite: ${photo.isFavorite}`);
  };
  
  const removePhoto = (index) => {
    photos.value.splice(index, 1);
  };
  </script>
  
  <style scoped>
  body {
    background-color: #efe2c7;
    font-family: monospace;
    padding: 20px;
    font-size: 16px;
  }
  
  .gallery {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 10px;
  }
  
  .no-photos {
    text-align: center;
    color: #999;
  }
  
  form {
    margin-bottom: 20px;
  }
  </style>
  