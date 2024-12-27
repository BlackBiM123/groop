<template>
    <section class="list-block">
        <div class="list-block-container container">
            <div class="list-block-image">
                <h2 class="hidden-title">{{ $t('listBlock.title') }}</h2>
                <img v-if="locale === 'ru'" src="@/assets/images/groop-ru.png" alt="list-block-image">
                <img v-else src="@/assets/images/groop-en.png" alt="list-block-image">
            </div>
            <div class="list-block-content">
                <h2>{{ $t('listBlock.title') }}</h2>
                <ul>
                    <li v-for="i in 8" :key="i">
                        <CustomIcon :name="icons[i - 1]" />
                        {{ $t(`listBlock.item${i}`) }}
                    </li>
                </ul>
                <button @click="scrollToTop" class="get-access">{{ $t('btn') }}</button>
            </div>
        </div>
    </section>
</template>

<script setup>
import CustomIcon from './CustomIcon.vue';
import { useI18n } from 'vue-i18n';

const { locale } = useI18n();

const icons = [
    'more',
    'mouse-square',
    'tg-black',
    'trend-up',
    'aim',
    'profile-2user',
    'message-text',
    'tick-circle'
];

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
    gap: 3rem;
    justify-content: space-between;
    .list-block-image{
            width: 52%;
            min-width: 52%;
            .hidden-title{
                font-size: 56px;
                font-weight: 600;
                line-height: 56px;
                color: #000;
                display:none;
            }
            img{
                width: 100%;
            }
    }

    .list-block-content{
        width: 48%;
        display: flex;
        flex-direction: column;
        gap: 1rem;
    
        h2{
            font-size: 56px;
            font-weight: 600;
            line-height: 56px;
            color: #000;
        }
        li{
            font-size: 16px;
            font-weight: 400;
            line-height: 20px;
            color: #000;
            margin:18px 0;
            display: flex;
            align-items: center;
            gap: 1rem;
        }
    }
}

@media (max-width: 1024px) {
    .list-block{
        padding: 5rem 0;
        .list-block-container{
            flex-direction: column;
            align-items: center;
            .list-block-image{
                width: 100%;
                max-width:520px;
                .hidden-title{
                    display:flex;
                    justify-content: center;
                    margin: 0 0 30px;
                    font-size: 40px;
                    line-height: 40px;
                }
            }
            .list-block-content{
                width:100%;
                max-width:520px;
                h2{
                    display:none;
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
}
</style> 