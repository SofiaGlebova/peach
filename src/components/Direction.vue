<template>
    <div class="direction">
        <h2 class="direction__title">Направления бизнеса</h2>
        <div class="direction-wrapper">
            <div class="direction__items">
                <div :class="['direction__item', {'show': trigger}]" id="id" v-for="(direction, index) in directions" :key="index">
                    <img :src="direction.img" alt="direction" id="id" :class="['direction__img', {'show': trigger}]">
                    <div class="effect" id="priority">
                        <div class="direction__item-title">
                        {{ direction.title }}
                            <div class="direction-dropdown" @click="toggleDescription(index)">
                                <svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 36 36" fill="none">
                                    <path d="M11.5713 14.7858L17.9999 21.2143L24.4284 14.7858" stroke="white" stroke-width="2"/>
                                </svg>
                            </div>
                        </div>  
                        <div class="direction__item-description">{{ direction.descr }}</div>  
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import cyber from '../assets/img/cyber.jpg'
import cloud from '../assets/img/cloud.jpg'
import man from '../assets/img/man.jpg'
import support from '../assets/img/support.jpg'
import im from '../assets/img/impor.jpg'

    const directions = [
        {id: 0, img: support, title:'Решения Softline', descr: 'ГК Softline предлагает клиентам собственную линейку оборудования (ПК, серверы, торговое оборудование и проч.), разработку программных продуктов, облачных решений, решений в области информационной безопасности.'},
        {id: 1, img: cyber, title:'Кибербезопасность', descr: 'Softline обладает всеми необходимыми государственными лицензиями для организации проектов по информационной безопасности и аттестации. '},
        {id: 2, img: im, title:'Импортозамещение', descr: 'ГК Softline обладает широчайшим портфелем решений и услуг для импортозамещения, включая ПО и оборудование собственного производства.'},
        {id: 3, img: cloud, title:'Облачные решения', descr: 'Softline использует современные облачные решения как российских, так и международных вендоров для масштабирования бизнеса своих клиентов. Подписки, услуги, трансформация.'},
        {id: 4, img: man, title:'Цифровая трансформация и разработка ПO', descr: 'Softline использует современные технологи и новые возможности для увеличения производительности бизнеса заказчика. В штате ГК Softline - 2000+ разработчиков, которые трансформируют ПО под нужды конкретного предприятия.'},
        {id: 5, img: support, title:'Техническая поддержка Softline', descr: '200+ инженеров, 24 часа в сутки, 7 дней в неделю, 12 месяцев в году, сервисное партнерство с 30+ мировыми производителями.'}
    ]

    const trigger = ref(false)

    const toggleDescription = (index) => {
        trigger.value = !trigger.value
  
    }
</script>

<style lang="scss" scoped>

@media screen and (max-width: 291px) {
.direction-dropdown {
    width: 24px;
    height: 24px;
    cursor: pointer;
}
.direction .direction__item-title {
    display: flex;
}
.direction-wrapper {
    padding: 0 5px;
}
.direction .direction__item-description {
    font-size: 16px;
    font-weight: 300;
}
.show#id {
    height: 240px;
}
}

.direction {
    &__img {
        height: 260px;
    }
    &__title {
        color: #444;
        text-align: center;
        font-family: Proxima Nova Condensed;
        font-size: 56px;
        font-style: normal;
        font-weight: 600;
        line-height: 100%; /* 56px */
        margin-top: 100px;
    }
    &__items {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 22px 20px;
        margin: 55px auto 0;
        width: 100%;
        padding: 0;

    }
    &__item {
        width: 100%;
        height: 260px;
        position: relative;
        display: inline-block;
        margin: 0;
        overflow: hidden; 
    }
    &__item-title {
        color: white;
        font-family: Proxima Nova Condensed;
        font-size: 24px;
        position: absolute;
        font-style: normal;
        font-weight: 600;
        line-height: 100%;
        padding: 28px 20px;
    }
    &__item-description {
        max-width: 480px;
        margin-top: 76px;
        margin-left: 20px;
        color: var(--1, #FFF);
        font-family: Proxima Nova Condensed;
        font-size: 17px;
        font-style: normal;
        font-weight: 400;
        line-height: 140%;
        
    }
.effect {
    // opacity: 0.6;
    background: rgba($color: #2D3653, $alpha: 0.6);
    position: absolute;
    top: 180px;
    left: 0;
    width: 100%;
    height: 100%;
    transition: all 0.4s ease-in-out;
}
.effect:hover {
    position: absolute;
    overflow: hidden;
    top: 0;
    left: 0;
}
}
</style>