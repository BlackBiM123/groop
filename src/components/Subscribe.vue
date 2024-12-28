<template>
  <section class="subscribe">
    <div class="container">
        <div class="subscribe-container">
            <div class="subscribe-content">
                <h2>{{ $t('subscribe.title') }}</h2>
                <p>{{ $t('subscribe.description') }}</p>
            </div>
            <div class="subscribe-btn">
                <a :href="tgUrl" target="_blank">
                    <span>{{ $t('subscribe.button') }}</span>
                    <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                      <path d="M8.55443 11.8675C8.37964 12.0171 8.27206 12.2305 8.25576 12.4599L8.04697 15.3983C8.03066 15.6278 8.22064 15.8295 8.42771 15.7292V15.7292C8.55573 15.6671 8.66778 15.5765 8.75522 15.4642L10.0082 14.266C10.3093 13.978 10.7736 13.9474 11.1099 14.1933L14.2108 16.4606C14.8814 16.8378 15.3554 16.6411 15.5392 15.8415L17.9542 4.51767C18.167 3.52136 17.606 3.12154 16.9353 3.37304L2.7483 8.80602C1.76811 9.19294 1.79068 9.73463 2.58386 9.9829L5.85277 10.999C6.0832 11.0706 6.33314 11.0421 6.54153 10.9204L14.3817 6.34264C14.7783 6.07502 15.1426 6.22334 14.846 6.48451L8.55443 11.8675Z" stroke="white" stroke-width="1.2" stroke-linecap="round"/>
                    </svg>
                </a>
            </div>
        </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import CustomIcon from './CustomIcon.vue';
import { computed } from 'vue';
import { useI18n } from 'vue-i18n';

const { locale } = useI18n();
const tgUrl = computed(() => {
  return locale.value === 'ru' ? 'https://t.me/groop_ru' : 'https://t.me/groop_eng';
});
</script>

<style scoped lang="scss">
.subscribe {
  background: #F7F7F7;
  text-align: center;

  .subscribe-container{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30px 0px;
  }
  .subscribe-content{
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
    h2{
        font-size: 26px;
        line-height: 30px;
        font-weight: 500;
    }
    p{
        font-size: 16px;
        line-height: 20px;
        font-weight: 400;
        text-align: left;
    }
  }
  .subscribe-btn{
    a{
        width:fit-content;
        background: #164DFF;
        color: #FFF;
        font-size: 16px;
        line-height: 20px;
        font-weight: 400;
        display: flex;
        height: 52px;
        padding: 0 30px;
        align-items: center;
        justify-content: center;
        border-radius: 26px;
        span{
            margin-right: 7px;
        }
    }
  }
}

@media (max-width: 768px) {
    .subscribe{
        .subscribe-container{
            padding: 20px 0px;
            gap:1rem;

        }
        .subscribe-content{
            gap:7px;
            h2{
                font-size: 20px;
                line-height: 24px;

            }
            p{
                font-size: 14px;
                line-height: 18px;
            }
            .subscribe-btn{
                a{
                    font-size: 16px;
                    line-height: 20px;
                }
            }
        }
    }
}

@media (max-width: 599px) {
    .subscribe{
        .subscribe-container{
            flex-direction: column;
            align-items: flex-start;
            gap:0;
        }
        .subscribe-content{

        }
        .subscribe-btn{
                width:100%;
                margin-top:17px;
            a{
                height:44px;
            }
        }
    }
}
</style>
