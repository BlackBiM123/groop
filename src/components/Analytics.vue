<template>
<section class="tasks" :class="locale" :style="{ '--image-path': imagePath }">
    <div class="tasks-container">
        <h2>{{ $t('analytics.title') }}</h2>
        <p class="description">{{ $t('analytics.description') }}</p>
        <div class="tasks-grid">
            <div class="task-card">
                <h3>{{ $t('analytics.card1.title') }}</h3>
                <p>{{ $t('analytics.card1.description') }}</p>
            </div>
            <div class="task-card">
                <h3>
                    {{ $t('analytics.card2.title') }}
                    <div class="info-container" ref="target">
                        <img src="@/assets/images/icon.png" alt="alert-circle" @click="isOpened = !isOpened" />
                        <div class="info-content">
                            <transition name="popup">
                                <ReportLibrary @close="isOpened = false" v-if="isOpened" />
                            </transition>
                        </div>
                    </div>
                </h3>
                <p>{{ $t('analytics.card2.description') }}</p>
            </div>
            <div class="task-card">
                <h3>{{ $t('analytics.card3.title') }}</h3>
                <p>{{ $t('analytics.card3.description') }}</p>
            </div>
            <div class="task-card">
                <h3>{{ $t('analytics.card4.title') }}</h3>
                <p>{{ $t('analytics.card4.description') }}</p>
            </div>
        </div>
    </div>
</section>
</template>

  
  
<script setup>
import CustomIcon from './CustomIcon.vue';
import {
    ref,
    computed
} from 'vue';
import {
    onClickOutside
} from '@vueuse/core'
import ReportLibrary from './ReportLibrary.vue';
import {
    useI18n
} from 'vue-i18n';

const {
    locale
} = useI18n();
const imagePath = computed(() => locale.value === 'ru' ? 'analytics' : 'analytics-en');

const target = ref(null)

onClickOutside(target, event => isOpened.value = false)
const isOpened = ref(false);
</script>
  
  
<style lang="scss" scoped>
.tasks {
    padding: 4rem 0;
    color: #fff;

    .info-container {
        position: relative;

        img {
            cursor: pointer;
        }

        .info-content {
            position: absolute;
            top: 40px;
            left: -20px;
        }
    }

    &.ru {
        .task-card {
            &:first-child {
                background-image: url('@/assets/images/analytics/item1.png');
            }

            &:nth-child(2) {
                background-image: url('@/assets/images/analytics/item2.png');
            }

            &:nth-child(3) {
                background-image: url('@/assets/images/analytics/item3.png');
            }

            &:nth-child(4) {
                background-image: url('@/assets/images/analytics/item4.png');
            }
        }
    }

    &.en {
        .task-card {
            &:first-child {
                background-image: url('@/assets/images/analytics-en/item1.png');
            }

            &:nth-child(2) {
                background-image: url('@/assets/images/analytics-en/item2.png');
            }

            &:nth-child(3) {
                background-image: url('@/assets/images/analytics-en/item3.png');
            }

            &:nth-child(4) {
                background-image: url('@/assets/images/analytics-en/item4.png');
            }
        }
    }
}

.tasks-container {
    width: 100%;
    max-width: 1750px;
    margin: 0 auto;
    padding: 0 15px;

    h2 {
        width: 970px;
        margin: 30px auto;
        font-size: 56px;
        font-weight: 500;
        line-height: 56px;
        text-align: center;
    }

    .description {
        font-size: 16px;
        font-weight: 400;
        line-height: 20px;
        color: #979797;
        text-align: center;
        margin: 0 auto;
        width: 720px;
    }
}

.tasks-grid {
    display: flex;
    gap: 1rem;
    margin-top: 5rem;
}

.task-card {
    background-color: #1F2329;
    padding: 35px 25px;
    border-radius: 32px;
    height: 500px;
    width: 420px;
    max-width: 420px;
    background-repeat: no-repeat;
    background-size: contain;

    &:first-child {
       
        background-size: 280px;
        background-position: center 190px
    }

    &:nth-child(2) {
     
        background-size: 700px;
        background-position: 0% 90px
    }

    &:nth-child(3) {
       
        background-size: 750px;
        background-position: 40% 110px
    }

    &:nth-child(4) {
      
        background-size: 340px;
        background-position: center 195px
    }

    h3 {
        font-size: 26px;
        line-height: 32px;
        font-weight: 500;
        margin-bottom: 10px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: 10px;
        width: 100%;

        img {
            cursor: pointer;

        }
    }

    p {
        color: #9c9c9e;
        font-weight: 400;
        line-height: 20px;
        font-size: 16px;
        letter-spacing: 0.01em;
    }
}

@media (max-width: 1440px) {
    .tasks-container {
        justify-content: center;
        width: 100%;
        max-width: 100%;

        h2 {
            max-width: 100%;
        }

        .tasks-grid {
            flex-wrap: wrap;
            justify-content: center;
            width: 100%;
        }

        .task-card {
            width: 45%;
            max-width: 520px;
        }
    }
}

@media (max-width: 1024px) {
    .tasks {
        padding: 2rem 0;
    }

    .tasks-container {
        justify-content: center;
        width: 100%;
        max-width: 100%;

        h2 {
            font-size: 40px;
            line-height: 42px;
        }

        .description {
            font-size: 16px;
            line-height: 20px;
            max-width: 100%;
        }

        .tasks-grid {
            flex-wrap: wrap;
            justify-content: center;
            width: 100%;
            margin-top: 4rem;
        }

        .task-card {
            width: 45%;
            max-width: 520px;
        }
    }
}

@media (max-width: 794px) {
    .tasks {
        .info-container {
            position: static;

            .info-content {
                left: 0px;
                width: 100%;
            }
        }
    }

    .tasks-container {
        .tasks-grid {
            position: relative;
        }
    }
}

@media (max-width: 768px) {
    .tasks-container {
        h2 {
            font-size: 30px;
            line-height: 32px;
        }

        .task-card {
            position: relative;
            width: 100%;
            max-width: 520px;
        }
    }
}

@media (max-width: 599px) {
    .tasks-container {
        .task-card {
            height: 400px;

            &:first-child {
                background-size: 220px;
                background-position: center 190px
            }

            &:nth-child(2) {
                background-size: 550px;
                background-position: 0% 90px
            }

            &:nth-child(3) {
                background-size: 550px;
                background-position: 40% 110px
            }

            &:nth-child(4) {
                background-size: 280px;
                background-position: center 195px
            }
        }
    }
}

@media (max-width: 375px) {
    .tasks-container {
        .task-card {
            h3 {
                font-size: 22px;
            }

            p {
                font-size: 14px;
            }
        }
    }
}
</style>

<style lang="scss">
.popup-enter-active,
.popup-leave-active {
    transition: all 0.3s ease;
}

.popup-enter-from,
.popup-leave-to {
    opacity: 0;
    transform: scale(0.5) translateY(-40px);
}

.popup-enter-to,
.popup-leave-from {
    opacity: 1;
    transform: scale(1) translateY(0);
}
</style>
