<template>
    <div class="slider">
        <div class="slides" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
            <div class="slide" v-for="(slide, index) in slides" :key="index">
                <img :src="slide.image" alt="" />
                <div class="overlay">
                    <h2>{{ slide.title }}</h2>
                    <p>{{ slide.subtitle }}</p>
                </div>
            </div>
        </div>

        <button class="prev" @click="prevSlide">&#10094;</button>
        <button class="next" @click="nextSlide">&#10095;</button>

        <div class="dots">
            <span v-for="(slide, index) in slides" :key="index" :class="{ active: currentSlide === index }"
                @click="goToSlide(index)">
            </span>
        </div>
    </div>
</template>

<script setup>
import { ref } from "vue";

const currentSlide = ref(0);

const slides = [
    {
        image: "https://optim.tildacdn.com/tild3031-6363-4338-b863-646132303039/-/format/webp/pyatno_na_kovre.jpg.webp",
        title: "Крупный цех по стирке ковров",
        subtitle: "Успешно работаем с 2015 года"
    },
    {
        image: "https://optim.tildacdn.com/tild3265-6664-4532-a363-393934306263/-/format/webp/sushka_kovrov.jpg.webp",
        title: "Сушильная камера для ковров",
        subtitle: "Высушим Ваш ковёр на 100%"
    },
    {
        image: "https://optim.tildacdn.com/tild6338-3032-4762-b763-363039633866/-/format/webp/kover_krasnodar.jpg.webp",
        title: "Специализированное оборудование",
        subtitle: "Применяется спец оборудование, моющие и чистящие средства"
    }
];

const nextSlide = () => {
    currentSlide.value = (currentSlide.value + 1) % slides.length;
};

const prevSlide = () => {
    currentSlide.value =
        (currentSlide.value - 1 + slides.length) % slides.length;
};

const goToSlide = (index) => {
    currentSlide.value = index;
};
</script>

<style scoped>
.slider {
    position: relative;
    width: 100%;
    height: 700px;
    margin: 0 auto;
    overflow: hidden;
}

.slides {
    display: flex;
    transition: transform 0.6s ease-in-out;
}

.slide {
    min-width: 100%;
    height: 700px;
    position: relative;
}

.slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    filter: brightness(0.25);
}

.overlay {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: #fff;
    text-align: center;
    text-shadow: 0 2px 8px rgba(0, 0, 0, 0.7);
    z-index: 4;
    width: 90%;
}

.overlay h2 {
    font-size: 32px;
    margin-bottom: 10px;
}

.overlay p {
    font-size: 18px;
}

.prev,
.next {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(0, 0, 0, 0.4);
    border: none;
    color: #fff;
    font-size: 28px;
    cursor: pointer;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    transition: background 0.3s ease;
}

.prev {
    left: 20px;
}

.next {
    right: 20px;
}

.prev:hover,
.next:hover {
    background: rgba(0, 0, 0, 0.7);
}

.dots {
    text-align: center;
    position: absolute;
    bottom: 15px;
    width: 100%;
    z-index: 4;
}

.dots span {
    display: inline-block;
    width: 12px;
    height: 12px;
    margin: 0 4px;
    padding: 5px;
    border: 2px solid #fff;
    border-radius: 50%;
    cursor: pointer;
    transition: background 0.3s ease;
}

.dots span:hover {
    background: #fff;
}

.dots .active {
    background: #fff;
}

@media (max-width: 1200px) {
    .slider {
        max-width: 100%;
        height: 600px;
    }

    .slide {
        height: 600px;
    }

    .overlay h2 {
        font-size: 28px;
    }

    .overlay p {
        font-size: 16px;
    }

    .prev,
    .next {
        width: 45px;
        height: 45px;
        font-size: 24px;
    }

    .dots span {
        width: 10px;
        height: 10px;
        margin: 0 3px;
    }
}

@media (max-width: 768px) {
    .slider {
        height: 500px;
    }

    .slide {
        height: 500px;
    }

    .overlay {
        width: 95%;
    }

    .overlay h2 {
        font-size: 24px;
        margin-bottom: 8px;
    }

    .overlay p {
        font-size: 14px;
    }

    .prev,
    .next {
        width: 40px;
        height: 40px;
        font-size: 20px;
    }

    .prev {
        left: 15px;
    }

    .next {
        right: 15px;
    }

    .dots {
        bottom: 10px;
    }

    .dots span {
        width: 8px;
        height: 8px;
        padding: 4px;
    }
}

@media (max-width: 480px) {
    .slider {
        height: 400px;
    }

    .slide {
        height: 400px;
    }

    .overlay h2 {
        font-size: 20px;
        margin-bottom: 6px;
    }

    .overlay p {
        font-size: 12px;
    }

    .prev,
    .next {
        width: 35px;
        height: 35px;
        font-size: 18px;
    }

    .prev {
        
        left: 10px;
    }

    .next {
        right: 10px;
    }

    .dots span {
        width: 7px;
        height: 7px;
        margin: 0 2px;
        padding: 3px;
    }
}

@media (max-width: 360px) {
    .slider {
        height: 350px;
    }

    .slide {
        height: 350px;
    }

    .overlay h2 {
        font-size: 15px;
    }

    .overlay p {
        font-size: 10px;
    }

    .prev,
    .next {
        width: 30px;
        height: 30px;
        font-size: 16px;
    }

    .prev {
        left: 8px;
    }

    .next {
        right: 8px;
    }

    .dots {
        bottom: 8px;
    }

    .dots span {
        width: 6px;
        height: 6px;
        padding: 2px;
    }
}
</style>