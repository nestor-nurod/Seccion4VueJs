<script setup>
import { onMounted, ref } from 'vue';

import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const postXpage = 10;

const posts = ref([]);
const start = ref(0);
const end = ref(postXpage);
const loading = ref(true);

const favorite = ref('');

const setFavorite = (post) => {
  favorite.value = post;
}

const nextPage = () => {
  start.value = start.value + postXpage;
  end.value = end.value + postXpage;
}

const previousPage = () => {
  start.value = start.value - postXpage;
  end.value = end.value - postXpage;
}

onMounted(async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  } finally {
    loading.value = false
  }

})

//fetch('https://jsonplaceholder.typicode.com/posts').then(res => res.json()).then(data => posts.value = data).finally(()=> loading.value=false);

</script>

<template>
  <LoadingSpinner v-if="loading" class="mt-5"></LoadingSpinner>
  <div class="container" v-else>
    <h1>App</h1>
    <div class="row">
      <h2 class="title"> Mi post favorito:
        <span v-if="favorite !== ''">{{ favorite }}</span>
        <span v-if="favorite === ''">Ninguno =(</span>
      </h2>

    </div>
    <PaginatePost :start="start" :end="end" :posts="posts.length" @previousPage="previousPage" @nextPage="nextPage"
      class="mb-2" />
    <div class="row">
      <div class="col-md-12" v-for="(post, index) in posts.slice(start, end)" :key="index">
        <BlogPost class="mb-2" :title="post.title" :id="post.id" :body="post.body" @setFavorite="setFavorite" />
      </div>
    </div>
  </div>
</template> 