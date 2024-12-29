<template>
  <section class="hero" :class="{ ru: isRussian, ready: isReady }">
    <!-- Звезды и кргуляшки статичные с паралаксом -->
    <!-- <StarField /> -->

    <!-- Звезды и кргуляшки анимация - снег-->

    <SnowField />
    <div class="hero-container">
      <h1><span class="name">Groop —</span>{{ $t('hero.title') }}</h1>
      <p>{{ $t('hero.subtitle') }}</p>
      <form class="hero-form" @submit.prevent="submitEmail">
        <input
          v-model="email"
          type="email"
          :placeholder="$t('hero.emailPlaceholder')"
          :disabled="isLoading"
        >
        <button
          type="submit"
          class="hero-button"
          :disabled="isLoading || !email"
        >
          {{ isLoading ? $t('hero.sending') : $t('btn') }}
        </button>
        <p v-if="error" class="info-line error-message">{{ $t('hero.serverError') }}</p>
        <p v-if="success" class="info-line success-message">{{ $t('hero.success') }}</p>
      </form>

    </div>
    <div class="hero-bottom-img">
      <img v-if="isRussian" src="@/assets/images/hero-bg.png" alt="Hero bottom">
      <img v-else src="@/assets/images/hero-bg-en.png" alt="Hero bottom">
    </div>

  </section>
</template>

<script setup>
import SnowField from './SnowField.vue';
import StarField from './StarField.vue';
import {
  computed, onMounted, ref, watch
} from 'vue';
import {
  useI18n
} from 'vue-i18n';

const { locale, t } = useI18n();
const isRussian = computed(() => locale.value === 'ru');
const isReady = ref(false);
const email = ref('');
const error = ref('');
const success = ref(false);
const isLoading = ref(false);

// Функция для очистки сообщений
const clearMessages = () => {
  error.value = '';
  success.value = false;
};

// Следим за изменениями error и success
watch([error, success], ([newError, newSuccess]) => {
  if (newError || newSuccess) {
    setTimeout(clearMessages, 3000);
  }
});

const validateEmail = (email) => {
  return String(email)
    .toLowerCase()
    .match(
      /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|.(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
    );
};

const submitEmail = async () => {
  clearMessages(); // Очищаем предыдущие сообщения перед новой отправкой

  if (!validateEmail(email.value)) {
    error.value = t('hero.invalidEmail');
    return;
  }

  isLoading.value = true;

  try {
    const response = await fetch('https://test.profdepo.ru/api/AppUsers/add-to-wish-list', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(email.value)
    });

    if (!response.ok) {
      throw new Error(t('hero.serverError'));
    }

    success.value = true;
    email.value = '';
  } catch (e) {
    error.value = e.message;
  } finally {
    isLoading.value = false;
  }
};

// Добавляем watch для locale
watch(locale, () => {
  isReady.value = false;
  setTimeout(() => {
    isReady.value = true;
  }, 1000);
});

onMounted(() => {
  setTimeout(() => isReady.value = true, 1000);
});

</script>

<style lang="scss" scoped>
.hero {
  width: 100%;
  min-height: 1080px;
  padding: 30px 0 0;
  text-align: center;
  background-color: #060606;
  position: relative;
  color: #FFF;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  .hero-form {
    position: relative;
  }
  .info-line {
    font-size: 12px;
    margin: 10px 0;
    position: absolute;
    width:100%;
    text-align: center;
    bottom:-40px;
    &.error-message {
      color: #ff4444;
    }
    &.success-message {
      color: #44ff44;
    }
  }
  &.ru {
    .hero-container {
      width: 1040px;
    }
  }

  .hero-container {
    //background-color: #060606;
    //box-shadow: 0 0 100px 50px #060606;
    position: relative;
    z-index: 3;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0 auto;
    height: 100%;
    width: 850px;
    flex-grow: 1;
  }

  &.ready {
    &::before {
      transform: translate(-50%, 0);
      animation: twinkle 5s infinite;
      transition: transform ease 3s;
    }
  }

  &::before {
    content: '';
    opacity: 0.8;
    position: absolute;
    bottom: -100px;
    left: 50%;
    transform: translate(-50%, 100%);
    width: 950px;
    height: 470px;
    box-shadow: 0 0 150px 30px rgba(255, 255, 255, 0.6);
    border-radius: 50%;
    z-index: 1;

  }

  .hero-container {
    position: relative;
    z-index: 3;

    .hero-form {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      max-width: 500px;
      width: 100%;
      background: #2c2c2F;
      border-radius: 28px;
      height: 56px;

      input {
        display: flex;
        flex-grow: 1;
        background: none;
        height: 100%;
        box-shadow: none;
        border: none;
        outline: none;
        color: #FFF;
        padding: 0 20px;
        font-size: 16px;
        font-weight: 400;
        min-width: 0;

        &:disabled {
          opacity: 0.7;
          cursor: not-allowed;
        }
      }

      .hero-button {
        background: #FFF;
        color: #1E1E1E;
        font-weight: 600;
        font-size: 16px;
        padding: 0 30px;
        height: 100%;
        border-radius: 28px;
        white-space: nowrap;

        &:disabled {
          opacity: 0.7;
          cursor: not-allowed;
        }
      }
    }
  }

  h1 {
    font-weight: 500;
    font-size: 60px;
    line-height: 68px;
    position: relative;
    //background-color: #060606;
    //box-shadow: 0px -20px 20px 20px #060606;

    span {
      position: relative;

      &::after {
        content: '';
        position: absolute;
        top: -10px;
        left: -30px;
        width: 67px;
        height: 42px;
        background-image: url('@/assets/images/newyear.png');
        background-size: 67px 42px;
        background-position: center;
        background-repeat: no-repeat;
      }
    }

  }

  p {
    font-weight: 400;
    font-size: 18px;
    line-height: 22px;
    width: 720px;
    margin: 35px auto;
    color: #b9b9b9;
    //background-color: #060606;
    //box-shadow: 0 0 100px 50px #060606;
  }

  .hero-bottom-img {

    height: 500px;
    overflow: hidden;
    position: relative;
    z-index: 5;
    opacity: 1;
    img{
      max-width:994px;
      width:100%;
      height:auto;
    }
  }
}

@keyframes twinkle {
  0% {
    opacity: 0.8;
    box-shadow: 0 0 150px 30px rgba(255, 255, 255, 0.6);
  }

  30% {
    opacity: 1;
    box-shadow: 0 0 150px 44px rgba(255, 255, 255, 0.6);
  }

  80% {
    opacity: 0.8;
    box-shadow: 0 0 150px 30px rgba(255, 255, 255, 0.6);
  }
}

@media (max-width: 991px) {
  .hero {
    height: 1024px;
    min-height: 1024px;
    .hero-form{
      .info-line{
        bottom:-50px;
      }
    }
    &::before {

      bottom: 0px;

    }

    &.ru {
      .hero-container {
        width: 100%;
      }
    }

    .hero-container {
      width: 100%;

      p {
        max-width: 90%;
        margin: 25px auto;
        padding: 0 5px;
      }
    }

    h1 {
      font-size: 42px;
      line-height: 42px;
      padding: 0 30px;

      span {

        &::after {
          left: -25px;
          width: 50px;
          height: 37px;
          background-size: contain;

        }
      }
    }

    .hero-bottom-img {
      width: 130%;
      height: 60%;
      min-height: 60%;

      img {
        height: auto;
      }

      height: 650px;

    }
  }
}

@media (max-width: 600px) {
  .hero {
    height: 812px;
    min-height: 812px;
    .hero-form{
      .info-line{
        bottom:-55px;
        font-size:12px;
        line-height: 14px;
      }
    }
    &::before {
      bottom: -200px;
    }

    .hero-container {
      padding: 0 15px;

      .hero-form {
        height: 46px;
        position: relative;
        button {
          font-size: 15px;
          padding: 0 15px !important;
        }

        input {
          font-size: 15px;
        }
      }

      h1 {
        font-size: 30px;
        line-height: 36px;
        padding: 0;

        span {

          &::after {
            left: -15px;
            width: 34px;
            height: 37px;
            background-size: contain;

          }
        }

      }

      p {
        font-size: 15px;
        margin: 15px auto 25px;
        padding: 0;
        max-width: 100%;
      }
    }

    .hero-bottom-img {
      width: 150%;
      height: 50%;
      min-height: 50%;

      img {
        height: auto;
      }

      height: 650px;

    }
  }
}

@media (max-width: 420px) {
  .hero {
    padding: 50px 0 0;

    .hero-bottom-img {
      height: 45%;
      min-height: 45%;
    }
  }
}

@media (max-width: 375px) {
  .hero {

    .hero-container {
      .hero-form {
        input {
          min-width: 0;
        }
      }
    }
  }
}

.error-message {
  color: #ff4444;
  font-size: 14px;
  margin-top: 10px;
}

.success-message {
  color: #44ff44;
  font-size: 14px;
  margin-top: 10px;
}
</style>
