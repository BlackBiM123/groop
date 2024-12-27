<template>
    <header class="header">
        <div class="header-content">
            <router-link to="/" class="logo">
                <h3><custom-icon name="logo" size="22" color="FFF" /> Groop</h3>
            </router-link>
            <div class="lang-dropdown" @click="toggleDropdown" ref="dropdownRef">
                <button class="dropdown-toggle">
                    {{ currentLocale.toUpperCase() }}
                    <CustomIcon name="chevron-down" color="000" size="12" :class="{ rotated: isOpen }" />
                </button>
                <div class="dropdown-menu" v-show="isOpen">
                    <button v-for="lang in ['en', 'ru']" :key="lang" :class="{ active: currentLocale === lang }"
                        @click="changeLocale(lang)">
                        {{ lang.toUpperCase() }}
                    </button>
                </div>
            </div>

        </div>
    </header>
</template>
  
<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import { useI18n } from 'vue-i18n';
import CustomIcon from './CustomIcon.vue';

const { locale } = useI18n();
const currentLocale = computed(() => locale.value);
const isOpen = ref(false);
const dropdownRef = ref(null);

const toggleDropdown = () => {
    isOpen.value = !isOpen.value;
};

const changeLocale = (lang) => {
    locale.value = lang;

};

const handleClickOutside = (event) => {
    if (dropdownRef.value && !dropdownRef.value.contains(event.target)) {
        isOpen.value = false;
    }
};

onMounted(() => {
    document.addEventListener('click', handleClickOutside);
});

onUnmounted(() => {
    document.removeEventListener('click', handleClickOutside);
});
</script>
  
<style scoped lang="scss">
  .header {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    
    z-index: 100;
    padding: 20px 40px;
  
    .header-content {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
  
    .logo {
      display: flex;
      align-items: center;
      text-decoration: none;
      
      h3 {
        display: flex;
        align-items: center;
        gap: 8px;
        font-weight: 400;
        color: #FFF;
        font-size: 21px;
        margin: 0;
      }
    }
  
    .lang-dropdown {
      position: relative;
      
      .dropdown-toggle {
        background: none;
        border: none;
        color: #FFF;
        font-size: 14px;
        font-weight: 500;
        padding: 8px 12px;
        cursor: pointer;
        display: flex;
        align-items: center;
        gap: 6px;
        transition: color 0.3s;
  
        &:hover {
          color: #FFF;
        }
  
        .custom-icon {
          transition: transform 0.3s ease;
          &.rotated {
            transform: rotate(180deg);
          }
        }
      }
  
      .dropdown-menu {
        position: absolute;
        top: 100%;
        right: 0;
        margin-top: 8px;
        background: rgba(0, 0, 0, 0.9);
        backdrop-filter: blur(10px);
        border-radius: 8px;
        border: 1px solid rgba(255, 255, 255, 0.2);
        overflow: hidden;
        min-width: 100px;
  
        button {
          width: 100%;
          background: none;
          border: none;
          color: #666;
          font-size: 14px;
          font-weight: 500;
          padding: 8px 16px;
          cursor: pointer;
          transition: all 0.3s;
          text-align: left;
  
          &:hover {
            color: #FFF;
            background: rgba(255, 255, 255, 0.1);
          }
  
          &.active {
            color: #FFF;
            background: rgba(255, 255, 255, 0.05);
          }
        }
      }
    }
  }

  @media (max-width: 600px) {
    .header {
      padding: 15px 15px;
      .lang-dropdown{
        .dropdown-toggle{
          padding: 8px 0 8px 10px;
        }
      }
    }
  }
  </style>