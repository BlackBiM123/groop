<template>
<section class="features" :class="{ ru: isRussian, 'is-visible': isVisible }">
    <div class="container">
        <h2>{{ $t('features.title') }} <span class="underlined">{{ $t('features.underlinedArea') }}</span></h2>
        <div class="features-grid">
            <div class="feature-card">
                <CustomIcon name="grammerly" color="FFF" />
                <h3>{{ $t('features.cards.card1.title') }}</h3>
                <p>{{ $t('features.cards.card1.description') }}</p>
            </div>
            <div class="feature-card">
                <CustomIcon name="elements" color="FFF" />
                <h3>{{ $t('features.cards.card2.title') }}</h3>
                <p>{{ $t('features.cards.card2.description') }}</p>
            </div>
            <div class="feature-card">
                <CustomIcon name="ranking" color="FFF" />
                <h3>{{ $t('features.cards.card3.title') }}</h3>
                <p>{{ $t('features.cards.card3.description') }}</p>
            </div>
        </div>
    </div>
</section>
</template>

<script setup>
import {computed, ref, onMounted, onUnmounted} from 'vue';
import { useI18n } from 'vue-i18n';
import CustomIcon from './CustomIcon.vue';

const { locale } = useI18n();
const isRussian = computed(() => locale.value === 'ru');
const isVisible = ref(false);
let observer = null;

onMounted(() => {
    observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
            isVisible.value = true;
            observer.disconnect();
        }
    }, {
        threshold: 0.5
    });

    observer.observe(document.querySelector('.features'));
});

onUnmounted(() => {
    if (observer) {
        observer.disconnect();
    }
});
</script>

<style lang="scss" scoped>
.features {
    padding: 4rem 0;
    background: #FFF;

    h2 {
        text-align: center;
        font-size: 30px;
        font-weight: 500;
        line-height: 36px;
        letter-spacing: 0em;
        text-align: left;
        max-width: 1100px;
        margin: 3rem auto 5rem;
        text-align: center;
    }

    &.ru {
        h2 {
            max-width: 1020px;
        }
        .underlined {
        position: relative;
        white-space: nowrap;

        &::after {
            content: '';
            
            width: 500px;
            height: 10px;
            background: url('@/assets/images/line1.png') no-repeat left center;
            background-size: 100% 100%;
        
            }
        }
    }

    .underlined {
        position: relative;
        white-space: nowrap;

        &::after {
            content: '';
            position: absolute;
            bottom: -15px;
            left: -20px;
            width: 400px;
            height: 20px;
            background: url('@/assets/images/line1.png') no-repeat left center;
            background-size: auto;
            opacity: 0;
            transform: scaleX(0);
            transform-origin: left;
            transition: transform 0.5s ease-out, opacity 0.3s;
        }
    }

    &.is-visible {
        .underlined::after {
            opacity: 1;
            transform: scaleX(1);
        }
    }
}

.features-grid {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 2rem;

    .feature-card {
        width: 402px;
        height: 516px;
        background: #000;
        border-radius: 32px;
        color: #FFF;
        padding: 20px;
        display: flex;
        flex-direction: column;

        h3 {
            font-size: 24px;
            font-weight: 500;
            line-height: 28px;
            letter-spacing: 0em;
            text-align: left;
            margin-top: 10px;
        }

        p {
            flex-grow: 1;
            display: flex;
            align-items: flex-end;
            color: #A3A3A3;
            font-size: 14px;
            line-height: 18px;
            letter-spacing: 0em;
            text-align: left;
        }

        &:first-child {
            background: #000 url('../assets/images/card-item1.png') no-repeat center center;
        }

        &:nth-child(2) {
            height: 548px;
            background: #000 url('../assets/images/card-bg.png') no-repeat center center;

            p {
                color: #FFF;
            }
        }

        &:last-child {
            background: #000 url('../assets/images/card-item2.png') no-repeat center center;
        }
    }
}

@keyframes draw {
    0% {
        width: 40px;
    }

    100% {
        width: 400px;
    }
}

@media (max-width: 768px) {
    .features {
        padding: 0.5rem 0;
        &.ru {
        
        .underlined {
            position: relative;
            white-space: nowrap;

            &::after {
                content: '';
                width: 320px;
                }
            }
        }
        h2 {
            font-size: 20px;
            line-height: 24px;
            max-width: 530px;
            margin-bottom: 3rem;

            .underlined {
                &::after {
                    content: '';
                    position: absolute;
                    bottom: -15px;
                    left: -5px;
                    width: 230px;
                    height: 10px;
                    background: url('@/assets/images/line1.png') no-repeat left center;
                    background-size: 100% 100%;
          
                    opacity: 1;
                    transform: scaleX(1);
                    
                    transform-origin: left;
                    transition: transform 0.5s ease-out, opacity 0.3s;
                }
            }
        }

        .features-grid {
            gap: 1rem;
            flex-direction: column;
            padding: 0 20px;

            .feature-card {
                width: 100%;
                height: 480px;
                align-items: center;

                h2 {
                    font-size: 24px;
                }

                p {
                    text-align: center;
                }

                &:nth-child(2) {
                    height: 480px;
                    background-size: 100% auto;
                    background-position: center center;
                }

                &:first-child {
                    background-size: 180px
                }

                &:last-child {
                    background-size: 180px
                }
            }
        }
    }
}

@media (max-width: 599px) {
    .features {
        .features-grid {
            padding: 0;
        }

        h2 {
            font-size: 18px;
            line-height: 20px;
            max-width: 480px;

            .underlined {

                
            }
        }

    }
}
@media (max-width: 385px) {
    .features {
        .features-grid {
            padding: 0;
            .feature-card{
                h3{
                    text-align: center;
                }
                &:nth-child(2) {
                    background-size: auto 100%;
                }
            }
        }
        &.ru {
        
        .underlined {
            &::after {
                content: '';
                width: 290px;
                }
            }
        }
    }
}
</style>