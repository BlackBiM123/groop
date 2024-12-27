<template>
  <section class="tasks" :class="locale">
    <div class="tasks-container">
        <h2>{{ $t('tasks.title') }}</h2>
        <p class="description">{{ $t('tasks.description') }}</p>
        <div class="tasks-grid">
            <div class="task-card">
                <h3>{{ $t('tasks.card1.title') }}</h3>
                <p>{{ $t('tasks.card1.description') }}</p>
            </div>
            <div class="task-card">
                <h3>{{ $t('tasks.card2.title') }}</h3>
                <p>{{ $t('tasks.card2.description') }}</p>
            </div>
            <div class="task-card">
                <h3>{{ $t('tasks.card3.title') }}</h3>
                <p>{{ $t('tasks.card3.description') }}</p>
            </div>  
            <div class="task-card">
                <h3>{{ $t('tasks.card4.title') }}</h3>
                <p>{{ $t('tasks.card4.description') }}</p>
            </div>  
        </div>
    </div>
  </section>
</template>

<script setup>
import { useI18n } from 'vue-i18n';

const { locale } = useI18n();
</script>

<style scoped lang="scss">
.tasks {
  padding: 4rem 0;
  color:#fff;
  &.en{
    .task-card{
      &:first-child{
        background-image: url('@/assets/images/tasks-en/task1.png');
      }
      &:nth-child(2){
        background-image: url('@/assets/images/tasks-en/task2.png');
      }
      &:nth-child(3){
        background-image: url('@/assets/images/tasks-en/task3.png');
      }
      &:nth-child(4){
        background-image: url('@/assets/images/tasks-en/task4.png');
      }
    }
  }
}
.tasks-container{
    width: 100%;
    max-width: 1750px;
    margin: 0 auto;
    padding:0 15px;
    h2{
        width:910px;
        margin: 30px auto;
        font-size:56px;
        font-weight: 500;
        line-height: 56px;
        text-align: center;
    }
    .description{
        font-size: 16px;
        font-weight: 400;
        line-height: 20px;
        color:#979797;
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
  padding:35px 25px;
  border-radius: 32px;
  height: 500px;
  width:420px;
  background-repeat: no-repeat;
  background-size: contain;
  &:first-child{
    background-image: url('@/assets/images/tasks/task1.png');
    background-position: center 230px
  }
  &:nth-child(2){
    background-image: url('@/assets/images/tasks/task2.png');
    background-size: 850px;
    background-position: 30% 150px
  }
  &:nth-child(3){
    background-image: url('@/assets/images/tasks/task3.png');
    background-position: center 230px
  }
  &:nth-child(4){
    background-image: url('@/assets/images/tasks/task4.png');
    background-size: 830px;
    background-position: 78% 195px
  }
  h3{
    font-size: 26px;
    line-height: 32px;
    font-weight: 500;
    margin-bottom: 10px;
  }
  p{
    color:#9c9c9e;
    font-weight: 400;
    line-height:20px;
    font-size: 16px;
    letter-spacing: 0.01em;
  }
}

@media (max-width: 1440px) {
    .tasks-container{
        justify-content: center;
        width:100%;
        max-width: 100%;
        h2{
            max-width: 100%;
        }
        .tasks-grid{
            flex-wrap: wrap;
            justify-content: center;
            width:100%;
        }
        .task-card{
            width: 45%;
            max-width: 520px;
        }
    }
}

@media (max-width: 1024px) {
    .tasks{
        padding: 2rem 0;
    }
    .tasks-container{
        justify-content: center;
        width:100%;
        max-width: 100%;
        h2{
            font-size: 40px;
            line-height: 42px;
        }
        .description{
            font-size: 16px;
            line-height: 20px;
            max-width: 100%;
        }
        .tasks-grid{
            flex-wrap: wrap;
            justify-content: center;
            width:100%;
            margin-top: 4rem;
        }
        .task-card{
            width: 45%;
            max-width: 520px;
        }
    }
}
@media (max-width: 768px) {
    .tasks-container{
        .task-card{
            width: 100%;
            max-width: 520px;
        }
    }
}
@media (max-width: 599px) {
    .tasks-container{
         .task-card{
            height:400px;
            &:first-child{
                background-size: 200px;
                background-position: center 200px
            }
            &:nth-child(2){
                background-size: 650px;
                background-position: 30% 130px
            }
            &:nth-child(3){
                background-size: 200px;
                background-position: center 180px
            }
            &:nth-child(4){
                background-size: 630px;
                background-position: 70% 155px
            }
         }
    }
}
@media (max-width: 375px) {
    .tasks-container{
         .task-card{
            h3{
                font-size:22px;
            }
            p{
                font-size:14px;
            }
         }
    }
}
</style> 