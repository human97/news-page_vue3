<script setup>
import NewsList from '@/components/News/NewsList.vue'
import AppLoader from '@/components/AppLoader.vue'
import AppButton from '@/components/AppButton.vue'
import { ref, onMounted } from 'vue'
import axios from 'axios'

const news = ref([])
const nav = ref({})
const isNewsLoading = ref(false)
const currentPage = ref(1)
const totalPages = ref(1)
const url = 'https://flems.github.io/test/api/news/'
const fetchNews = async () => {
  try {
    isNewsLoading.value = true
    const response = await axios.get(`${url}`)
    news.value = response.data.items
    nav.value = response.data.nav
    totalPages.value = response.data.nav.total
    currentPage.value = response.data.nav.current
  } catch (error) {
    console.log(error)
  } finally {
    isNewsLoading.value = false
  }
}

const loadMoreNews = async () => {
  try {
    isNewsLoading.value = true
    const response = await axios.get(`${url}${currentPage.value + 1}/`)
    news.value = [...news.value, ...response.data.items]
    nav.value = response.data.nav
    totalPages.value = response.data.nav.total
    currentPage.value = response.data.nav.current
  } catch (error) {
    console.log(error)
  } finally {
    isNewsLoading.value = false
  }
}

onMounted(async () => {
  await fetchNews()
})
</script>

<template>
  <main class="news">
    <div class="header-news">
      <h1 class="header-news__title">Новости</h1>
    </div>

    <news-list
      v-if="news.length" 
      :items="news"
      :nav="nav"
    />

    <app-loader 
      v-show="isNewsLoading"
    />

    <app-button 
      v-show="currentPage < totalPages"
      @click="loadMoreNews"
      class="btn-load"
    >
      Загрузить ещё
    </app-button>
  </main>
</template>

<style scoped lang="scss">
.news {
  position: relative; 
  

}
.header-news {
  position: relative;
  height: 320px;
  background-image: url('/images/news.webp');
  background-repeat: no-repeat;
  background-size: cover;

  &__title {
    position: absolute;
    bottom: 48px;
    left: 100px;
    font-weight: 700;
    font-size: 40px;
    line-height: 48px;
    color: #17171A;
  }
}

.container {
  margin: 64px 100px 200px 100px;
}

.btn-load {
    position: absolute;
    bottom: 102px;
    left: 50%;
    transform: translateX(-50%);
}
</style>