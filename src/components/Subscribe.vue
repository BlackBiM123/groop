<template>
  <section class="subscribe">
    <div class="container">
        <div class="subscribe-container">
            <div class="subscribe-content">
                <h2>{{ $t('subscribe.title') }}</h2>
                <p>{{ $t('subscribe.description') }}</p>
            </div>
            <div class="subscribe-btn">
                <a href="https://t.me/lentadnya" target="_blank">
                    <span>{{ $t('subscribe.button') }}</span>
                    <CustomIcon name="tg"/>
                </a>
            </div>
        </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import CustomIcon from './CustomIcon.vue';
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