<template>
  <footer class="footer">
    <div class="container">
        <div class="footer-content">
            <div class="footer-left">
                <h3><custom-icon name="logo" size="36" color="FFF"/> Groop</h3>
                <p class="description">{{ $t('footer.description') }}</p>
                <button @click="scrollToTop" class="get-access light">{{ $t('btn') }}</button>
                <p class="copyright">&copy;2024 Profdepo</p>
            </div>
            <div class="footer-right">
                <span class="label">{{ $t('footer.socials') }}</span>
                <a href="https://t.me/lentadnya" target="_blank">Telegram</a>
            </div>
        </div>
    </div>
  </footer>
</template>
<script setup>
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
.footer {
  padding: 4rem 0 2rem;
  color:#FFF;

  h3{
    font-size: 36px;
    font-weight: 400;
    line-height: 41px;
    display:flex;
    align-items: center;
    gap: 12px;
  }
  .description{
    font-size: 16px;
    font-weight: 400;
    line-height: 20px;
    color:#8c8c8c;
    margin: 15px 0;
  }
  .get-access{
    margin: 30px 0;
  }
  .copyright{
    font-size: 14px;
    font-weight: 400;
    line-height: 18px;
    color:#8c8c8c;
    margin: 50px 0 0;
  }
}
.footer-right{
    display:flex;
    flex-direction: column;
    gap: 20px;
    padding-top:50px;
    padding-right: 50px;
    span{
        font-size:12px;
        line-height: 14px;
        color:#fff;
    }
    a{
        font-size: 16px;
        font-weight: 400;
        line-height: 20px;
        color:#8c8c8c;
        &:hover{
            color:#FFF;
        }
    
    }
}
.footer-content {
  display:flex;
  justify-content: space-between;
}

@media (max-width: 1024px) {
    .footer{
        padding: 2rem 0;
        position: relative;
        .footer-content{
            flex-direction: column;
            align-items: center;
            .footer-left{
                width:100%;
                display:flex;
                flex-direction: column;
                align-items: center;
                .description{
                    text-align: center;
                    max-width: 320px;
                }
                .copyright{
                    position: absolute;
                    right:35px;
                    bottom:2rem;
                }
            }
            .footer-right{
               width:100%;
               padding:0 35px;
               gap:10px;
            }
        }
    }
}
@media (max-width: 599px) {
    .footer{
        .footer-content{
            .footer-right{
                padding:0 5px;
            }
            .footer-left{
                .copyright{
                    right:15px;
                }
            }
        }
    }
}
</style> 