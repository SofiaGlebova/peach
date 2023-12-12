<template>
    <div class="mission">
        <div class="mission__bg">
            <img src="../assets/icons/mission-left.png" alt="left icon" class="mission__bg-icon left">
            <img src="../assets/icons/mission-right.png" alt="right icon" class="mission__bg-icon right">
        </div>
        <div class="mission__content">
           <h2 class="mission__content-header">Миссия Softline</h2> 
           <div class="mission__content-description">Мы помогаем организациям трансформироваться, работать эффективно и безопасно в условиях цифровой экономики.</div>
        </div>
    </div>
</template>

<style lang="scss">
@import '../assets/styles/variables.scss';
.mission { 
    position:relative;
    &__bg {
        min-height: 471px;
        background: $main-color;  
        position: relative;  
        &-icon {
            position: absolute;
            width: 24%;
            top: 10%;
        }
    }
    &__content {
        position: absolute; 
        bottom: 140px;
        padding-left: 68px;
        padding-right: 72px;
    }
    &__content-header {
        color: #FFF;
        text-align: center;
        font-size: 56px;
        font-style: normal;
        font-weight: 600;
        line-height: 100%;
        margin-bottom: 40px;
    }
    &__content-description {
        color: #FFF;
        text-align: center;
        font-size: 32px;
        font-style: normal;
        font-weight: 400;
        line-height: 150%; /* 48px */
    }
    .right {
        right: 0;
    }
}
</style>