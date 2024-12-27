<template>
<div class="report-library" :style="popupStyle" ref="popup">
    <h2>{{ $t('report.title') }}
        <CustomIcon class="close-icon" name="close" @click="emit('close')" />
    </h2>
    <div class="lists">
        <ul>
            <li v-for="item in 7" :key="item">{{item}}. {{ $t('report.item' + item) }}</li>
        </ul>
        <ul>
            <li v-for="item in 10" :key="item">{{item + 7}}. {{ $t(`report.item${item + 7}`) }}</li>
        </ul>
    </div>
</div>
</template>

<script setup>
import {
    useI18n
} from 'vue-i18n';
import {
    ref,
    onMounted,
    computed
} from 'vue';
import CustomIcon from './CustomIcon.vue';

const emit = defineEmits(['close']);
const {
    t
} = useI18n();
const popup = ref(null);

const popupStyle = computed(() => {
    if (!popup.value) return {};
    if (window.innerWidth < 794) return {};

    const rect = popup.value.getBoundingClientRect();
    const windowWidth = window.innerWidth;
    const windowHeight = window.innerHeight;
    let style = {};


    if (rect.right > windowWidth) {
        style.right = '-60px';
        style.left = 'auto';
    }


    if (rect.bottom > windowHeight) {
        style.bottom = '50px';
        style.top = 'auto';
    }

    return style;
});

onMounted(() => {

    popup.value?.getBoundingClientRect();
});
</script>

<style lang="scss" scoped>
.report-library {
    position: absolute; 
    width: 700px;
    background-color: #FFF;
    padding: 20px;
    border-radius: 25px;
    z-index: 1000; 

    h2 {
        color: #000;
        font-size: 18px;
        font-weight: 500;
        line-height: 20px;
        margin-bottom: 15px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding-right:3px;
    }

    .close-icon {
        cursor: pointer;

    }

    .lists {
        display: flex;
        gap: 10px;
    }

    ul {
        display: flex;
        width: 50%;
        flex-direction: column;
        gap: 5px;

        li {

            color: #000;
            font-weight: 300;
            font-size: 14px;
            line-height: 18px;
        }
    }
}

@media (max-width: 794px) {
    .report-library {
        left: 0;
        transform: translateY(30px);
        width: 100%;

    }
}

@media (max-width: 768px) {
    .report-library {
        width: 100%; // Адаптивная ширина для мобильны
        ul{
            li{
                font-size:12px;
            }
        }
    }
}
</style>
