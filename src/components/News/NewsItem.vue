<script setup>
import { computed } from 'vue'
import { format, fromUnixTime } from 'date-fns'
import { ru } from 'date-fns/locale'

const props = defineProps({
  item: {
    type: Object,
    required: true,
    default: () => ({})
  }
})

const formattedDate = computed(() => {
  const date = fromUnixTime(props.item.date);
  return {
    day: format(date, 'd', { locale: ru }),
    month: format(date, 'LLLL', { locale: ru }),
    year: format(date, 'yyyy', { locale: ru }),
  }
})
</script>

<template>
  <div class="news-item">
    <img v-if="item.image" class="news-item__img" :src="item.image" alt="news">

    <div class="container">
      <div class="news-item__date">
          <span class="news-item__date-day">{{ formattedDate.day }}</span>
          <div class="wrapper">
            <span class="news-item__date-month">{{ formattedDate.month }}</span>  
            <span class="news-item__date-year">{{ formattedDate.year }}</span>
          </div>
      </div>
      
      <h2 class="news-item__title">{{ item.name }}</h2>

      <p class="news-item__text">{{ item.previewText }}</p>

      <a class="news-item__link" href="#">{{ item.type.value }}</a>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.news-item {
    position: relative;
    max-width: 536px;
    min-height: 554px;
    border: 1px solid #0F62FE;
    border-radius: 16px;
    margin-bottom: 64px;

  &__img {
    max-width: 100%;
    height: 250px;
    border-radius: 16px 16px 0px 0px;
  }

  &__date {
    height: 36px;
    display: flex;
    align-items: center;
    gap: 4px;
    color: #A1A7B5;
    margin-bottom: 16px;

    &-day {
      font-weight: 400;
      font-size: 36px;
      line-height: 36px;
    }

    .wrapper {
      display: block;
      font-weight: 700;
      font-size: 15px;
      line-height: 16.5px;

      span {
        display: block;
      }
    }
  }

  &__title {
      font-weight: 400;
      font-size: 22px;
      line-height: 26.4px;
      color: #0C5BEF;
      margin-bottom: 16px;
    }

  &__text {
    font-weight: 400;
    font-size: 20px;
    line-height: 26px;
    color: #222327;
  }

  &__link {
    position: absolute;
    bottom: 32px;
    left: 32px;
    height: 28px;
    padding: 4px 15px;
    background: #F0F6FE;
    border-radius: 36px;
    font-weight: 400;
    font-size: 14px;
    color: #00133A;
    text-decoration: none;
  }
}
.container {
  padding: 32px 32px 92px 32px;
}
</style>