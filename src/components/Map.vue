<template>
    <div class="map">
        <div class="container">
            <div class="map-nav">
                <h2 class="map-nav__main-title">Офисы Softline</h2>
                <button @click="toggleDropdown" :class="['map-nav__main-icon', {['rotate']: isActive}]">
                    <svg @click="toggleMobileDropdown" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none">
                        <path d="M2.10156 7.99683L12.1016 16.0179L22.1016 7.99683" stroke="#444444" stroke-width="3"/>
                    </svg>
                </button>

                <div :class="['mobile__dropdown', {'mobile': mobileActive}]">
                    <template
                        v-for="(value, name, index) in regions" 
                        :key="index"
                    >
                        <div :class="['region', {'red': addMarkRegion}]" v-if="!['Все'].includes(name)">
                            {{ name }}
                            <div class="mobile__btn" @click="toggleCitiesDropdown(name)">
                                <svg xmlns="http://www.w3.org/2000/svg" width="8" height="4" viewBox="0 0 8 4" fill="none">
                                    <path d="M4 4L7.4641 0.25H0.535898L4 4Z" fill="#444444"/>
                                </svg>
                            </div>
                            <div :class="['region__cities', {'drop-cities': citiesActive}]" 
                                v-if="name !== 'Москва'">
                                <div
                                    v-for="city in value"
                                    :key="city.name"
                                >
                                    {{ city.name }}
                                </div>
                            </div>
                        </div>
                    </template>
                </div>

                <div :class="[
                    'dropdown', 
                    {  ['active']: isActive }
                ]" >
                    <div class="dropdown__container">
                        <template 
                            v-for="(value, name, index) in regions" 
                            :key="index"
                        >
                            <div
                                v-if="!['Все'].includes(name)"
                                class="regions" 
                            >
                                <div class="region">
                                {{ name }}
                                    <div class="region__cities" 
                                    v-if="name !== 'Москва'">
                                        <div 
                                            
                                            v-for="city in value"
                                            :key="city.name"
                                        >
                                            {{ city.name }}
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </template>
                    </div>
                </div>
            </div>
            <div :class="['map__tabs', {'white': isActive}]" >
                <button  
                    class="map__tabs-menu" 
                    v-for="(value, name, index) in regions" 
                    :key="index"
                >
                    <div @click="() => onSelectRegion(name)" :class="['map-tab', {['activeRegion']: selectedRegion === name}]">{{ name }}</div>
                </button>
            </div>  
        </div>
        <div class="map__position-city">
            <div :class="['map-img', {'white': isActive}]">
            <template 
                v-for="(value, name, index) in regions"                
                :key="index"
            >
                <template v-if="selectedRegion === 'Все' || selectedRegion === name">
                    <div
                        v-for="city in value"
                        :key="city.name"
                        class="coordinates" 
                        :style="{top:`${city.position.y}px`, left:`${city.position.x}px`}"
                    >
                    {{city.name}}
                    </div>
                </template>
            </template>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
    const getCityObject = (name, x, y) => {
        return {
            name,
            position: {
                x,
                y
            }
        }
    }
    const isActive = ref(false)
    const mobileActive = ref(false)
    const citiesActive = ref(false)
    const addMarkRegion = ref(false)
    const selectedRegion = ref('Все')

    const toggleDropdown = () => {
        isActive.value = !isActive.value
    }
    const toggleMobileDropdown = () => {
        mobileActive.value = !mobileActive.value
    }
    const toggleCitiesDropdown = (region) => {
        citiesActive.value = !citiesActive.value
        if (region) {
            console.log(region)
            
           addMarkRegion.value = !addMarkRegion.value 
        }
        
    }
    
    const onSelectRegion = (value) => {
        selectedRegion.value = value
    }

    const regions = {
        'Все': [],
        'Москва': [
            getCityObject('Москва', 123, 236)
        ],
        'Центр': [
            getCityObject('Воронеж', 74, 258),
            getCityObject('Ярославль', 154, 210),
            getCityObject('Белгород', 70, 288),
        ],
        'Северо-Запад': [
            getCityObject('Санкт-Петербург', 109, 145),
            getCityObject('Калининград', 10, 137)
        ],
        'Юг': [
            getCityObject('Ростов-на-Дону', 42, 332),
            getCityObject('Краснодар', 24.3, 390),
            getCityObject('Волгоград', 85, 373)
            
        ],
        'Волга': [
            getCityObject('Казань', 234, 310),
            getCityObject('Самара', 171, 318),
            getCityObject('Уфа', 244, 347),
            getCityObject('Оренбург', 197, 377),
            getCityObject('Нижний Новгород', 163, 272)
        ],
        'Урал': [
            getCityObject('Екатеринбург', 288, 340),
            getCityObject('Челябинск', 291, 374),
            getCityObject('Пермь', 364, 311),
            getCityObject('Сургут', 418, 323),
            getCityObject('Тюмень', 392, 375),
            getCityObject('Ижевск', 310, 301),
        ],
        'Сибирь': [
            getCityObject('Новосибирск', 480, 465),
            getCityObject('Омск', 446, 485),
            getCityObject('Томск', 563, 443),
            getCityObject('Красноярск', 606, 467),
            getCityObject('Иркутск', 670, 500)
        ],
        'Дальний Восток': [
            getCityObject('Хабаровск', 954, 481),
            getCityObject('Владивосток', 937, 586)
        ]
    }
</script>

<style lang="scss" scoped>
.container {
    display: flex;
    position: relative;
    box-shadow: 0px 0px 40px 0px rgba(0, 0, 0, 0.06);
}
.map-nav {
    display: flex;
    flex-wrap: wrap;
    gap: 0 16px;
    padding: 28px 0 28px 70px;
    &__main-title {
        color: #444;
        font-family: Proxima Nova Condensed;
        font-size: 24px;
        font-style: normal;
        font-weight: 600;
        line-height: 100%;
    }
    &__main-icon {
        border: none;
        background-color: white;
        cursor: pointer;
        transition: all 0.4s ease-in-out;
    }
}
.map__tabs-menu {
    border: none;
    background: white;
    cursor: pointer;
}
.map__tabs {
    padding: 30px 70px 0;
    display: flex;
    gap: 30px;
    align-items: flex-start;
}
.map-tab {
    color: #444;
    font-family: Proxima Nova Condensed;
    font-size: 18px;
    font-style: normal;
    font-weight: 600;
    line-height: 20px;
    height: 54px;
}
.map-img {
    background-image: url('../assets/img/map.svg');
    height: 601px;
    background-repeat: no-repeat;
    margin: 90px 29px 100px;
    position: relative;
    
}
.region {
    display: flex;
    flex-direction: column;
    gap: 10px;
    font-weight: 600;
    font-size: 18px;
    color: #444;
    line-height: 20px;
    position: relative;
    &__cities {
        display: flex;
        flex-direction: column;
        gap: 10px;  
        font-weight: 400; 
    }
}
.coordinates {
    position: absolute;
    color: #444;
    text-align: right;
    font-family: Proxima Nova Condensed;
    font-size: 14px;
    font-style: normal;
    font-weight: 600;
    line-height: 100%; /* 14px */
}
.coordinates::after {
    content: '';
    display: block;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: #444;
    position: absolute;
    top: -75%;
    left: 43%;
}
.dropdown {
    position: absolute;
    background-color: white;
    width: 100%;
    top: 70px;
    left: 0; 
    opacity: 0;
    box-shadow: 0px 0px 32px 0px rgba(0, 0, 0, 0.06);
    transition: all 0.4s ease-out;
    z-index: 1;
    
    &__container {
        display: flex;
        gap: 24px;
        justify-content: center;
        padding: 43px 0 17px;
    }
}
.active {
    opacity: 1;
    top: 100px;
}
.activeRegion {
    color: #A30C33;
    border-bottom: 3px solid #A30C33;
}
.rotate {
    transform: scale(1, -1);
    transition: all 0.3s ease-out;
}
.white {
    opacity: 0.2;
}
.mobile__dropdown {
    opacity: 0;
    height: 0;
}

</style>