<template>
    <section class="pricing">
        <div class="container">
            <h2>{{ $t('pricing.title') }}</h2>
            <p class="subtitle">{{ $t('pricing.description') }}</p>

            <div class="pricing-grid">
                <!-- Basic Plan -->
                <div class="pricing-card basic">
                    <div class="card-header">
                        <span class="plan-name">Basic</span>
                        <h3 class="price">{{ $t('pricing.basic.price') }}</h3>
                    </div>
                    <div class="card-content">
                        <ul>
                            <li><custom-icon name="pricing-1" />{{ $t('pricing.basic.item1') }}</li>
                            <li><custom-icon name="pricing-2" />{{ $t('pricing.basic.item2') }}</li>
                            <li><custom-icon name="profile-2user" />{{ $t('pricing.basic.item3') }}</li>
                            <li><custom-icon name="pricing-4" color="000" />{{ $t('pricing.basic.item4') }}</li>
                            <li><custom-icon name="pricing-5" />{{ $t('pricing.basic.item5') }}</li>
                        </ul>
                    </div>
                </div>

                <!-- Micro Team Plan -->
                <div class="pricing-card micro">
                    <div class="card-header">
                        <span class="plan-name">Micro Team</span>
                        <h3 class="price">{{ $t('pricing.micro.price') }}</h3>
                    </div>
                    <div class="card-content">
                        <ul>
                            <li><custom-icon name="pricing-1" color="FFF" />{{ $t('pricing.micro.item1') }}</li>
                            <li><custom-icon name="pricing-2" color="FFF" />{{ $t('pricing.micro.item2') }}</li>
                            <li><custom-icon name="profile-2user" color="FFF" />{{ $t('pricing.micro.item3') }}</li>
                            <li><custom-icon name="pricing-4" color="FFF" />{{ $t('pricing.micro.item4') }}</li>
                            <li><custom-icon name="pricing-5" color="FFF" />{{ $t('pricing.micro.item5') }}</li>
                        </ul>
                    </div>
                </div>

                <!-- Pro Plan -->
                <div class="pricing-card pro">
                    <div class="card-header">
                        <div class="recommended">{{ $t('pricing.recommended') }}</div>
                        <span class="plan-name">Pro</span>
                        <h3 class="price">{{ $t('pricing.pro.price') }}</h3>
                    </div>
                    <div class="card-content">
                        <ul>
                            <li><custom-icon name="pricing-1" />{{ $t('pricing.pro.item1') }}</li>
                            <li><custom-icon name="pricing-2" />{{ $t('pricing.pro.item2') }}</li>
                            <li><custom-icon name="profile-2user" />{{ $t('pricing.pro.item3') }}</li>
                            <li><custom-icon name="pricing-4" />{{ $t('pricing.pro.item4') }}</li>
                            <li><custom-icon name="pricing-5" />{{ $t('pricing.pro.item5') }}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import CustomIcon from '@/components/CustomIcon.vue';
import { useI18n } from 'vue-i18n';

const { locale } = useI18n();
</script>

<style scoped lang="scss">
.pricing {
  padding: 12rem 0;
  background: #FFF;

  h2 {
    text-align: center;
    font-size: 56px;
    font-weight: 600;
    margin-bottom: 20px;
  }

  .subtitle {
    text-align: center;
    color: #666;
    margin-bottom: 48px;
    font-size: 16px;
    line-height: 20px;
  }
}

.pricing-grid {
  display: flex;
  justify-content: space-between;
  gap: 24px;
  width:100%;
  margin: 0 auto;
}

.pricing-card {
  width:400px;
  max-width: 400px;
  border-radius: 24px;
  overflow: hidden;
  background: #FFF;
  background-color:#f7f7f7;
  &.basic {
    .card-header {
        background-image: url('@/assets/images/price/item1.png');
      background-size: 100%;
      background-position: center;
    }
  }
  &.micro {
    background-color:#1e1e1e;
    .card-header {
        background-image: url('@/assets/images/price/item2.png');
      background-size: 100%;
      background-position: center;
    }
    .card-content{
      ul{
        li{
          color:#fff;
        }
      }
    }
  }
  &.pro {
    .card-header {
        background-image: url('@/assets/images/price/item3.png');
      background-size: 100%;
      background-position: center;
    }
  }
  .card-header {
    padding: 32px;
    color: #FFF;
    position: relative;
    height: 240px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .recommended {
      position: absolute;
      top: 16px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(255, 255, 255, 0.2);
      padding: 4px 12px;
      border-radius: 16px;
      font-size: 14px;
    }

    .plan-name {
      font-size: 12px;
      line-height: 18px;
      font-weight: 500;
      display: block;
      margin-bottom: 15px;
    }

    .price {
      font-size: 35px;
      font-weight: 700;
    }
  }

  .card-content {
    padding: 10px 15px;

    ul {
      list-style: none;
      padding: 0;
      margin: 0;

      li {
        color: #333;
        font-size: 16px;
        font-weight: 400;
        line-height: 20px;
        margin:15px 0;
        display: flex;
        align-items: center;
        gap: 10px;
      }
    }
  }
}

@media (max-width: 1024px) {
  .pricing{
    padding: 5rem 0;
    h2{
      font-size: 40px;
      line-height: 42px;
    }
    .subtitle{
      font-size: 16px;
      line-height: 20px;
    }
  }
  .pricing-grid{
    flex-direction: column;
    align-items: center;    
    width:100%;
  }
  .pricing-card{
    max-width:520px;
    width:100%;
  }
}
@media (max-width: 599px) {
    .pricing{
        padding: 3rem 0;
        .subtitle{
            max-width: 320px;
            margin: 0 auto 2rem;
        }
    }
}
</style> 