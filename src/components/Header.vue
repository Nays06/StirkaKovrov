<template>
  <header>
    <div class="cont">
      <div>
        <img src="/Images/Header/logo.png" alt="Логотип" class="logo" />
        Стираем ковры с удовольствием
      </div>

      <div>
        <div class="location">
          <img
            src="/Images/Header/marker_location_place_where.svg"
            alt="Локация"
            class="image"
          />
          <div>
            Краснодар, Дмитрия Благоева 29
            <br />
            с 08:00 до 20:00 без выходных
          </div>
        </div>
        <div class="phone">
          <img
            src="/Images/Header/phone_contact_call_ring.svg"
            alt="Телефон"
            class="image"
          />
          <div>
            <a href="tel:8-938-488-33-11">8-938-488-33-11</a>
            <br />
            <a href="tel:8-861-292-22-33">8-861-292-22-33</a>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {};
</script>

<style scoped>
header {
  height: 110px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.cont {
  width: 96%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.cont > div:first-child {
  font-size: 18px;
  display: flex;
  align-items: center;
}

.cont > div:last-child {
  display: flex;
  align-items: center;
}

.logo {
  width: 220px;
  margin-right: 35px;
}

.location {
  display: flex;
  align-items: center;
  font-weight: 300;
  font-size: 18px;
  line-height: 1.55;
}

.phone {
  display: flex;
  align-items: center;
  margin-left: 40px;
}

.phone a {
  text-decoration: none;
  font-size: 24px;
  font-weight: 300;
  color: inherit;
  border-bottom: 0px solid var(--secondary-color);
  -webkit-box-shadow: inset 0px -1px 0px 0px var(--secondary-color);
  -moz-box-shadow: inset 0px -1px 0px 0px var(--secondary-color);
  box-shadow: inset 0px -1px 0px 0px var(--secondary-color);
}

.image {
  width: 35px;
  margin-right: 10px;
}

@media (max-width: 1200px) {
  .cont {
    padding: 0 20px;
  }

  .logo {
    width: 180px;
    margin-right: 20px;
  }

  .cont > div:first-child {
    font-size: 16px;
  }

  .location {
    font-size: 16px;
  }

  .phone {
    margin-left: 20px;
  }

  .phone a {
    font-size: 20px;
  }

  .image {
    width: 30px;
  }
}

@media (max-width: 768px) {
  header {
    height: auto;
    padding: 20px 0;
  }

  .cont {
    flex-direction: column;
    align-items: center;
    gap: 20px;
  }

  .cont > div:first-child {
    flex-direction: column;
    text-align: center;
  }

  .logo {
    width: 150px;
    margin-right: 0;
    margin-bottom: 10px;
  }

  .cont > div:last-child {
    flex-direction: column;
    align-items: center;
    gap: 15px;
  }

  .phone {
    margin-left: 0;
  }

  .location,
  .phone {
    font-size: 14px;
    text-align: center;
  }

  .phone a {
    font-size: 18px;
  }
}

@media (max-width: 480px) {
  .cont {
    padding: 0 15px;
  }

  .cont > div:first-child {
    font-size: 14px;
  }

  .logo {
    width: 120px;
  }

  .location {
    font-size: 13px;
  }

  .phone a {
    font-size: 16px;
  }

  .image {
    width: 25px;
  }
}
</style>