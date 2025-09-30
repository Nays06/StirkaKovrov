<template>
    <div class="title">{{ title }}</div>
    <div class="subtitle">{{ subtitle }}</div>
</template>

<script>
export default {
    props: {
        title: {
            type: String
        },
        subtitle: {
            type: String
        }
    }
}
</script>

<style scoped>
.title {
    font-size: 46px;
    line-height: 1.17;
    font-weight: 600;
    text-align: center;
}

.subtitle {
    font-size: 22px;
    line-height: 1.45;
    font-weight: 300;
    margin-top: 25px;
    margin-bottom: 10px;
    text-align: center;
}

@media (max-width: 1200px) {
    .title {
        font-size: 40px;
    }

    .subtitle {
        font-size: 20px;
        margin-top: 20px;
    }
}

@media (max-width: 768px) {
    .title {
        font-size: 32px;
        line-height: 1.2;
    }

    .subtitle {
        font-size: 18px;
        margin-top: 15px;
        margin-bottom: 8px;
    }
}

@media (max-width: 480px) {
    .title {
        font-size: 28px;
    }

    .subtitle {
        font-size: 16px;
        margin-top: 12px;
    }
}

@media (max-width: 360px) {
    .title {
        font-size: 24px;
        line-height: 1.25;
    }

    .subtitle {
        font-size: 14px;
        margin-top: 10px;
        margin-bottom: 6px;
    }
}
</style>