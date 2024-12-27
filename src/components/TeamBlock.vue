<template>
    <section class="list-block">
      <div class="list-block-container container">
          
          <div class="list-block-content">
              <h2>{{ $t('team.title') }}</h2>
              <p class="description">{{ $t('team.description') }}</p>
              <button @click="scrollToTop" class="get-access">{{ $t('btn') }}</button>
          </div>
          <div class="list-block-image">
              <img v-if="locale === 'ru'" src="@/assets/images/team-ru.png" alt="list-block-image">
              <img v-else src="@/assets/images/team-en.png" alt="list-block-image">
          </div>
      </div>
    </section>
  </template>
  
  <script setup lang="ts">
  import CustomIcon from './CustomIcon.vue';
  import { useI18n } from 'vue-i18n';

  const { locale } = useI18n();
  const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
};
  </script>
  
  <style scoped lang="scss">
  .list-block {
    padding: 12rem 0 8rem;
    background: #FFF;
  }
  .list-block-container{
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 3rem;
      .list-block-image{
            width: 55%;
            min-width: calc(55% - 3rem);
            img{
                width: 100%;
            }
    }
    .list-block-content{
        width: 45%;
        min-width: 45%;
          display: flex;
          flex-direction: column;
          gap: 1rem;
          h2{
              font-size: 50px;
              font-weight: 600;
              line-height: 56px;
              color: #000;
          }
          .description{
            font-size: 16px;
            font-weight: 400;
            line-height: 20px;
            color: #7c7c7c;
            margin:15px 0;
            width:470px;
            max-width:100%;
          }
          li{
              font-size: 16px;
              font-weight: 500;
              line-height: 20px;
              color: #000;
              margin:15px 0;
              display: flex;
              align-items: center;
              gap: 0.5rem;
          }
      }
  }

  @media (max-width: 1024px) {
    .list-block{
        padding: 5rem 0;
    }
    .list-block-container{
        flex-direction: column;
        .list-block-image{
            order: -1;
            width: 100%;
            max-width: 520px;
        }
        .list-block-content{
            width: 100%;
            max-width: 520px;
            h2{
                font-size: 40px;
                line-height: 42px;
            }
            .description{
                font-size: 16px;
                line-height: 20px;
            }
            .get-access{
                    margin: 0 auto;
                    width:100%;
                    height:50px;
                    font-size: 16px;
                    line-height: 20px;
                }
        }
    }
  }
  </style> 