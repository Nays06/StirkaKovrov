<template>
    <footer class="footer">
        <div class="footer-container">
            <div class="footer-left">
                <div class="footer-logo">
                    <img src="/Images/Footer/logo.png" alt="Логотип" class="logo" />
                </div>
                <p class="rights">© Все права защищены</p>
                <p class="tags">
                    #стиркаквров #чисткаквров #химчисткаквров <br />
                    #мойкаквров #краснодар
                </p>
            </div>

            <div class="footer-menu">
                <h4>МЕНЮ</h4>
                <ul>
                    <li><a href="#">Сертификаты безопасности</a></li>
                    <li><a href="#">Политика конфиденциальности</a></li>
                    <li><a href="#">Условия заказа и оказания услуг</a></li>
                </ul>
            </div>

            <p class="slogan">Стираем ковры с удовольствием✌</p>
            <div class="footer-right">
                <p class="seo-text">
                    Нас ищут по таким запросам: химчистка ковров Восток, стирка ковров в Краснодаре, чистка ковров,
                    почистить ковёр, мойка ковра, стирка паласов, химчистка, оверлок, реставрация ковра, удалить запах,
                    грязь и пятна с ковра, постирать ковёр с вывозом и доставкой
                </p>
            </div>
        </div>
    </footer>
</template>

<script setup>
</script>

<style scoped>
.footer {
    background: #111;
    color: #ccc;
    padding: 60px 0 80px 0;
    font-family: Arial, sans-serif;
    margin-top: 60px;
}

.footer-container {
    display: flex;
    justify-content: space-between;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

.footer-left {
    flex: 1 1 30%;
    min-width: 250px;
}

.footer-logo {
    display: flex;
    align-items: center;
    margin-bottom: 15px;
}

.footer-logo .logo {
    width: 200px;
    margin-right: 10px;
}

.rights {
    color: #525252;
    margin-top: 21px;
    font-size: 12px;
}

.tags {
    color: #525252;
    font-size: 12px;
}

.footer-menu {
    flex: 1 1 25%;
    min-width: 200px;
}

.footer-menu h4 {
    color: #525252;
    font-weight: 600;
    font-size: 16px;
    margin-bottom: 14px;
}

.footer-menu ul {
    list-style: none;
    padding: 0;
}

.footer-menu li {
    margin-bottom: 10px;
}

.footer-menu a {
    color: #fff;
    text-decoration: none;
    border-bottom: 0px solid #ff3503;
    -webkit-box-shadow: inset 0px -1px 0px 0px #ff3503;
    -moz-box-shadow: inset 0px -1px 0px 0px #ff3503;
    box-shadow: inset 0px -1px 0px 0px #ff3503;
    font-size: 14px;
    line-height: 1.55;
    transition: 0.5s;
}

.footer-menu a:hover {
    color: #ff3503;
}

.slogan {
    font-size: 14px;
    width: 300px;
    color: #8a8484;
    line-height: 1.55;
    font-weight: 300;
}

.seo-text {
    color: rgb(130, 130, 130);
    font-size: 13px;
    line-height: 1.55;
    font-weight: 300;
    width: 260px;
}

@media (max-width: 1200px) {
    .footer-container {
        max-width: 100%;
        padding: 0 15px;
    }

    .footer-left,
    .footer-menu,
    .slogan,
    .footer-right {
        flex: 1 1 45%;
        margin-bottom: 30px;
    }

    .footer-logo .logo {
        width: 180px;
    }

    .slogan {
        width: 100%;
        max-width: 250px;
    }

    .seo-text {
        width: 100%;
        max-width: 250px;
    }
}

@media (max-width: 768px) {
    .footer {
        padding: 40px 0 60px 0;
    }

    .footer-container {
        flex-direction: column;
        align-items: center;
        text-align: center;
    }

    .footer-left,
    .footer-menu,
    .slogan,
    .footer-right {
        flex: 1 1 100%;
        min-width: 0;
        margin-bottom: 20px;
    }

    .footer-logo {
        justify-content: center;
    }

    .footer-logo .logo {
        width: 150px;
    }

    .footer-menu h4 {
        font-size: 14px;
    }

    .footer-menu a {
        font-size: 13px;
    }

    .slogan {
        font-size: 13px;
        max-width: 100%;
    }

    .seo-text {
        font-size: 12px;
        max-width: 100%;
    }
}

@media (max-width: 480px) {
    .footer {
        padding: 30px 0 40px 0;
        margin-top: 30px;
    }

    .footer-container {
        padding: 0 10px;
    }

    .footer-logo .logo {
        width: 120px;
    }

    .rights,
    .tags {
        font-size: 11px;
    }

    .footer-menu h4 {
        font-size: 13px;
    }

    .footer-menu a {
        font-size: 12px;
    }

    .slogan {
        font-size: 12px;
    }

    .seo-text {
        font-size: 11px;
    }
}
</style>