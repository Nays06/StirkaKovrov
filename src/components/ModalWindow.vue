<template>
    <div class="gallery-grid">
        <div v-for="(image, index) in images" :key="index" class="gallery-item" @click="openModal(index)">
            <img :src="image.small" :alt="`Пример работы ${index + 1}`" class="gallery-image" loading="lazy">
        </div>
    </div>

    <transition name="modal-fade">
        <div v-if="isModalOpen" class="modal-overlay" @click="closeModal">
            <div class="modal-content" @click.stop :class="{ 'modal-visible': isModalVisible }">

                <button class="modal-close" @click="closeModal">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                        <path d="M18 6L6 18M6 6L18 18" stroke="currentColor" stroke-width="2" />
                    </svg>
                </button>

                <button class="modal-arrow modal-arrow-left" @click="prevSlide">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                        <path d="M15 18L9 12L15 6" stroke="currentColor" stroke-width="2" />
                    </svg>
                </button>

                <div class="carousel-container">
                    <div class="carousel-track" :style="{ transform: `translateX(${translateX}px)` }">
                        <div v-for="(slide, index) in carouselSlides" :key="index" class="carousel-slide">
                            <img :src="getLargeImageUrl(slide.originalIndex)"
                                :alt="`Пример работы ${slide.originalIndex + 1}`" class="modal-image"
                                :class="{ 'active': currentCarouselIndex === index }"
                                @load="onImageLoad(slide.originalIndex)">
                        </div>
                    </div>
                </div>

                <button class="modal-arrow modal-arrow-right" @click="nextSlide">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                        <path d="M9 18L15 12L9 6" stroke="currentColor" stroke-width="2" />
                    </svg>
                </button>

                <div v-if="!isImageLoaded" class="image-loader">
                    <div class="loader-spinner"></div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
export default {
    name: 'ImageGallery',
    data() {
        return {
            images: [
                {
                    small: 'https://optim.tildacdn.com/tild6362-6135-4436-b936-353062633366/-/resize/500x400/-/format/webp/chistka_kover_krasno.png.webp?7',
                    large: 'https://static.tildacdn.com/tild6362-6135-4436-b936-353062633366/chistka_kover_krasno.png'
                },
                {
                    small: 'https://optim.tildacdn.com/tild6362-6135-4436-b936-353062633366/-/resize/500x400/-/format/webp/chistka_kover_krasno.png.webp?7',
                    large: 'https://static.tildacdn.com/tild6362-6135-4436-b936-353062633366/chistka_kover_krasno.png'
                },
                {
                    small: 'https://optim.tildacdn.com/tild6362-6135-4436-b936-353062633366/-/resize/500x400/-/format/webp/chistka_kover_krasno.png.webp?7',
                    large: 'https://static.tildacdn.com/tild6362-6135-4436-b936-353062633366/chistka_kover_krasno.png'
                },
                {
                    small: 'https://optim.tildacdn.com/tild6362-6135-4436-b936-353062633366/-/resize/500x400/-/format/webp/chistka_kover_krasno.png.webp?7',
                    large: 'https://static.tildacdn.com/tild6362-6135-4436-b936-353062633366/chistka_kover_krasno.png'
                },
                {
                    small: 'https://optim.tildacdn.com/tild6362-6135-4436-b936-353062633366/-/resize/500x400/-/format/webp/chistka_kover_krasno.png.webp?7',
                    large: 'https://static.tildacdn.com/tild6362-6135-4436-b936-353062633366/chistka_kover_krasno.png'
                },
                {
                    small: 'https://optim.tildacdn.com/tild6362-6135-4436-b936-353062633366/-/resize/500x400/-/format/webp/chistka_kover_krasno.png.webp?7',
                    large: 'https://static.tildacdn.com/tild6362-6135-4436-b936-353062633366/chistka_kover_krasno.png'
                },
                {
                    small: 'https://optim.tildacdn.com/tild6362-6135-4436-b936-353062633366/-/resize/500x400/-/format/webp/chistka_kover_krasno.png.webp?7',
                    large: 'https://static.tildacdn.com/tild6362-6135-4436-b936-353062633366/chistka_kover_krasno.png'
                },
                {
                    small: 'https://optim.tildacdn.com/tild6362-6135-4436-b936-353062633366/-/resize/500x400/-/format/webp/chistka_kover_krasno.png.webp?7',
                    large: 'https://static.tildacdn.com/tild6362-6135-4436-b936-353062633366/chistka_kover_krasno.png'
                },
            ],
            isModalOpen: false,
            isModalVisible: false,
            currentIndex: 0,
            currentCarouselIndex: 0,
            translateX: 0,
            slideWidth: 0,
            isAnimating: false,
            isImageLoaded: false,
            loadedImages: new Set()
        };
    },
    computed: {
        carouselSlides() {
            const slides = [];

            slides.push({
                originalIndex: this.images.length - 1,
                isClone: true
            });

            this.images.forEach((_, index) => {
                slides.push({
                    originalIndex: index,
                    isClone: false
                });
            });

            slides.push({
                originalIndex: 0,
                isClone: true
            });

            return slides;
        }
    },
    mounted() {
        window.addEventListener('resize', this.updateSlideWidth);
    },
    beforeUnmount() {
        window.removeEventListener('resize', this.updateSlideWidth);
        document.removeEventListener('keydown', this.handleKeydown);
        document.body.style.overflow = '';
    },
    methods: {
        getLargeImageUrl(index) {
            return this.images[index].large;
        },

        updateSlideWidth() {
            if (this.isModalOpen) {
                const carouselContainer = document.querySelector('.carousel-container');
                if (carouselContainer) {
                    this.slideWidth = carouselContainer.offsetWidth;
                    this.translateX = -(this.currentCarouselIndex) * this.slideWidth;
                }
            }
        },

        openModal(index) {
            this.currentIndex = index;
            this.isImageLoaded = this.loadedImages.has(index);
            this.isModalOpen = true;
            document.body.style.overflow = 'hidden';
            document.addEventListener('keydown', this.handleKeydown);
            this.currentCarouselIndex = index + 1;

            this.$nextTick(() => {
                this.updateSlideWidth();
                setTimeout(() => {
                    this.isModalVisible = true;
                }, 10);
            });
        },

        closeModal() {
            this.isModalVisible = false;
            setTimeout(() => {
                this.isModalOpen = false;
                document.body.style.overflow = '';
                document.removeEventListener('keydown', this.handleKeydown);
            }, 300);
        },

        nextSlide() {
            if (this.isAnimating) return;

            this.isAnimating = true;
            this.isImageLoaded = false;
            this.currentIndex = (this.currentIndex + 1) % this.images.length;
            this.currentCarouselIndex++;

            if (this.loadedImages.has(this.currentIndex)) {
                this.isImageLoaded = true;
            }

            this.translateX = -this.currentCarouselIndex * this.slideWidth;

            if (this.currentCarouselIndex >= this.carouselSlides.length - 1) {
                setTimeout(() => {
                    this.currentCarouselIndex = 1;
                    this.translateX = -this.currentCarouselIndex * this.slideWidth;
                    this.isAnimating = false;
                }, 10);
            } else {
                setTimeout(() => {
                    this.isAnimating = false;
                }, 10);
            }
        },

        prevSlide() {
            if (this.isAnimating) return;

            this.isAnimating = true;
            this.isImageLoaded = false;
            this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length;
            this.currentCarouselIndex--;

            if (this.loadedImages.has(this.currentIndex)) {
                this.isImageLoaded = true;
            }

            this.translateX = -this.currentCarouselIndex * this.slideWidth;

            if (this.currentCarouselIndex <= 0) {
                setTimeout(() => {
                    this.currentCarouselIndex = this.carouselSlides.length - 2;
                    this.translateX = -this.currentCarouselIndex * this.slideWidth;
                    this.isAnimating = false;
                }, 10);
            } else {
                setTimeout(() => {
                    this.isAnimating = false;
                }, 10);
            }
        },

        onImageLoad(index) {
            this.loadedImages.add(index);
            if (index === this.currentIndex) {
                this.isImageLoaded = true;
            }
        },

        handleKeydown(event) {
            switch (event.key) {
                case 'Escape':
                    this.closeModal();
                    break;
                case 'ArrowLeft':
                    this.prevSlide();
                    break;
                case 'ArrowRight':
                    this.nextSlide();
                    break;
            }
        }
    },
    watch: {
        isModalOpen(newVal) {
            if (newVal) {
                setTimeout(() => {
                    this.updateSlideWidth();
                }, 50);
            }
        }
    }
};
</script>

<style scoped>
.gallery-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 15px;
    width: 98%;
    margin: 0 auto;
    background-color: white;
    padding: 20px;
}

.gallery-item {
    cursor: zoom-in;
    transition: transform 0.3s ease;
    overflow: hidden;
}

.gallery-image {
    width: 100%;
    object-fit: cover;
    border-radius: 0 !important;
    transition: transform 0.3s ease;
}

.gallery-item:hover .gallery-image {
    transform: scale(1.05);
}

.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.modal-content {
    position: relative;
    width: 100%;
    height: 100%;
    max-width: 1200px;
    max-height: 90vh;
    margin: 0 auto;
}

.carousel-container {
    width: 100%;
    height: 100%;
    overflow: hidden;
    position: relative;
}

.carousel-track {
    display: flex;
    height: 100%;
    transition: transform 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.carousel-slide {
    flex: 0 0 auto;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal-image {
    width: auto;
    height: auto;
    max-width: 95%;
    max-height: 95%;
    object-fit: contain;
    border-radius: 0 !important;
    box-shadow: none;
}

.modal-close {
    position: absolute;
    top: 20px;
    right: 20px;
    border: none;
    width: 40px;
    height: 40px;
    color: #333;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
    z-index: 1001;
    background: rgba(255, 255, 255, 0.8);
}

.modal-close:hover {
    background: rgba(255, 255, 255, 1);
}

.modal-arrow {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(255, 255, 255, 0.8);
    border: none;
    width: 40px;
    height: 40px;
    color: #333;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
    z-index: 1001;
}

.modal-arrow:hover {
    background: rgba(255, 255, 255, 1);
}

.modal-arrow-left {
    left: 20px;
}

.modal-arrow-right {
    right: 20px;
}

.image-loader {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 1002;
}

.loader-spinner {
    width: 40px;
    height: 40px;
    border: 3px solid #f3f3f3;
    border-top: 3px solid #333;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}

@keyframes spin {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}

.modal-fade-enter-active,
.modal-fade-leave-active {
    transition: opacity 0.3s ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
    opacity: 0;
}

.modal-content {
    opacity: 0;
    transform: scale(0.95);
    transition: all 0.3s ease;
}

.modal-visible {
    opacity: 1;
    transform: scale(1);
}

@media (max-width: 1200px) {
    .gallery-grid {
        grid-template-columns: repeat(3, 1fr);
        gap: 12px;
        padding: 15px;
    }

    .modal-content {
        max-width: 90%;
    }

    .modal-image {
        max-width: 90%;
        max-height: 85%;
    }
}

@media (max-width: 768px) {
    .gallery-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 10px;
        padding: 10px;
    }

    .modal-content {
        max-width: 95%;
        max-height: 80vh;
    }

    .modal-close,
    .modal-arrow {
        width: 35px;
        height: 35px;
    }

    .modal-close {
        top: 15px;
        right: 15px;
    }

    .modal-arrow-left {
        left: 15px;
    }

    .modal-arrow-right {
        right: 15px;
    }

    .modal-image {
        max-width: 100%;
        max-height: 80%;
    }

    .loader-spinner {
        width: 35px;
        height: 35px;
    }
}

@media (max-width: 480px) {
    .gallery-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 8px;
        padding: 8px;
    }

    .modal-content {
        max-width: 100%;
        max-height: 75vh;
    }

    .modal-close,
    .modal-arrow {
        width: 30px;
        height: 30px;
    }

    .modal-close svg,
    .modal-arrow svg {
        width: 20px;
        height: 20px;
    }

    .modal-close {
        top: 10px;
        right: 10px;
    }

    .modal-arrow-left {
        left: 10px;
    }

    .modal-arrow-right {
        right: 10px;
    }

    .modal-image {
        max-width: 100%;
        max-height: 70%;
    }

    .loader-spinner {
        width: 30px;
        height: 30px;
    }
}

@media (max-width: 360px) {
    .gallery-grid {
        gap: 6px;
        padding: 6px;
    }

    .modal-content {
        max-height: 70vh;
    }

    .modal-close,
    .modal-arrow {
        width: 25px;
        height: 25px;
    }

    .modal-close svg,
    .modal-arrow svg {
        width: 18px;
        height: 18px;
    }

    .loader-spinner {
        width: 25px;
        height: 25px;
    }
}
</style>