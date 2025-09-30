<template>
    <div class="slider-container">
        <div class="slider">
            <button class="nav-btn prev" @click="prevSlide">‹</button>

            <div class="slides-container">
                <div class="slides" :style="sliderStyle">
                    <div class="slide" v-for="(slide, index) in slides" :key="index">
                        <div class="img">
                            <img :src="slide.img" alt="carpet" />
                        </div>
                        <div class="content">
                            <div class="title">{{ slide.title }}</div>
                            <div class="text">{{ slide.text }}</div>
                            <Button style="margin-top: 30px;" />
                        </div>
                    </div>
                </div>
            </div>

            <button class="nav-btn next" @click="nextSlide">›</button>
        </div>
    </div>
</template>

<script setup>
import Button from "./Button.vue";
import { ref, computed, onMounted, onUnmounted } from "vue";

const currentSlide = ref(0);

const slides = [
    {
        img: "https://static.tildacdn.com/tild3939-3335-4139-b161-633564363464/obrezka_kovra.jpg",
        title: "Реставрация ковров от 500 руб.",
        text: "Ремонт ковров специалистами компании Восток. С радостью подарим вторую жизнь Вашему ковру.",
    },
    {
        img: "https://static.tildacdn.com/tild3939-3335-4139-b161-633564363464/obrezka_kovra.jpg",
        title: "Реставрация ковров от 500 руб.",
        text: "Ремонт ковров специалистами компании Восток. С радостью подарим вторую жизнь Вашему ковру.",
    },
    {
        img: "https://static.tildacdn.com/tild3939-3335-4139-b161-633564363464/obrezka_kovra.jpg",
        title: "Реставрация ковров от 500 руб.",
        text: "Ремонт ковров специалистами компании Восток. С радостью подарим вторую жизнь Вашему ковру.",
    },
];

const sliderStyle = computed(() => {
    return {
        transform: `translateX(-${currentSlide.value * 100}%)`,
        transition: "transform 0.6s ease",
    };
});

let intervalId = null;

function startInterval() {
    if (intervalId) {
        clearInterval(intervalId);
    }
    intervalId = setInterval(() => {
        nextSlide();
    }, 5000);
}

function prevSlide() {
    currentSlide.value = (currentSlide.value - 1 + slides.length) % slides.length;
    resetInterval()
}

function nextSlide() {
    currentSlide.value = (currentSlide.value + 1) % slides.length;
    resetInterval()
}

function resetInterval() {
    if (intervalId) {
        clearInterval(intervalId);
    }
    intervalId = setInterval(() => {
        nextSlide();
    }, 5000);
}

onMounted(() => {
    startInterval();
    window.addEventListener('resize', handleResize);
});

onUnmounted(() => {
    if (intervalId) {
        clearInterval(intervalId);
    }
    window.removeEventListener('resize', handleResize);
});
</script>

<style scoped>
.slider-container {
    text-align: center;
    padding: 30px;
    overflow: hidden;
}

.slider {
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
}

.slides-container {
    overflow: hidden;
    position: relative;
    width: 100%;
    max-width: 1200px;
}

.slides {
    display: flex;
    width: 100%;
}

.slide {
    width: 100%;
    flex-shrink: 0;
    display: flex;
    padding: 15px;
    border-radius: 8px;
    box-sizing: border-box;
}

.img {
    flex: 0 0 55%;
    height: 475px;
    overflow: hidden;
}

.img img {
    object-fit: cover;
    width: 100%;
    height: 100%;
}

.content {
    padding: 0 40px;
    text-align: left;
    flex: 1;
}

.title {
    font-size: 46px;
    line-height: 1.23;
    margin-bottom: 28px;
    font-weight: 600;
}

.text {
    font-size: 20px;
    line-height: 1.55;
    font-weight: 300;
}

.nav-btn {
    background: none;
    border: 2px solid #000;
    border-radius: 50%;
    font-size: 30px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    margin: 0 15px;
    flex-shrink: 0;
}

.nav-btn:hover {
    background: #ddd;
}

@media (max-width: 1200px) {
    .slides-container {
        max-width: 900px;
    }
    
    .img {
        flex: 0 0 50%;
        height: 400px;
    }
    
    .title {
        font-size: 36px;
    }
    
    .text {
        font-size: 18px;
    }
}

@media (max-width: 992px) {
    .slides-container {
        max-width: 700px;
    }
    
    .slide {
        flex-direction: column;
        text-align: center;
    }
    
    .img {
        flex: none;
        width: 100%;
        height: 350px;
        margin-bottom: 20px;
    }
    
    .content {
        padding: 0 20px;
        text-align: center;
    }
    
    .title {
        font-size: 32px;
    }
}

@media (max-width: 768px) {
    .slider-container {
        padding: 15px;
    }
    
    .slides-container {
        max-width: 500px;
    }
    
    .img {
        height: 280px;
    }
    
    .title {
        font-size: 28px;
        margin-bottom: 15px;
    }
    
    .text {
        font-size: 16px;
    }
    
    .nav-btn {
        width: 40px;
        height: 40px;
        font-size: 24px;
        margin: 0 10px;
    }
}

@media (max-width: 576px) {
    .slides-container {
        max-width: 330px;
    }
    
    .img {
        height: 220px;
    }
    
    .title {
        font-size: 24px;
    }
    
    .text {
        font-size: 14px;
    }
    
    .nav-btn {
        width: 40px;
        height: 40px;
        font-size: 20px;
        margin: 0 5px;
        position: absolute;
        margin-top: -40px;
        z-index: 1;
        background-color: #fff;
    }

    .prev {
        left: 10px;
    }

    .next {
        right: 10px;
    }
    
    .content {
        padding: 0 10px;
    }
}
</style>