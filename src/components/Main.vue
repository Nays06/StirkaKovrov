<template>
  <main>
    <section id="block1">
      <div class="title">Профессиональная стирка ковров</div>
      <div class="description">
        Вывоз, доставка и подъём <br />
        до квартиры — 0 рублей!
      </div>
      <div class="form">
        <PhoneInput v-model="phone" default-country="RU" @validation="handleValidation" ref="phoneInput" />
        <input type="button" value="Оставить заявку" @click="submitForm" :disabled="!isFormValid"
          :class="{ 'button-disabled': !isFormValid }" />
      </div>
      <div class="text">
        Перезвоним, произведём расчёт <strong>со скидкой 20%</strong> и ответим
        на все вопросы
      </div>
    </section>

    <section id="block2">
      <TitleSubtitle :title="'Удалим грязь, пятна и запахи'"
        :subtitle="'12 этапов стирки и сушка на 100% в специальной сушильной камере'" />
      <div class="video">
        <video autoplay playsinline loop muted>
          <source src="https://cdnv.boomstream.com/balancer/vE9v0K2Z-ehgC52Pl.mp4" type="video/mp4" />
        </video>
      </div>
      <div class="list">
        <div v-for="(list, index) in lists" :key="index">
          <img :src="list.src" :alt="list.text" />
          {{ list.text }}
        </div>
      </div>
      <Button style="margin-top: 30px;" />
      <div class="text">
        Перезвоним, произведём расчёт <strong>со скидкой 20%</strong> и ответим
        на все вопросы
      </div>
    </section>

    <section id="block3">
      <TitleSubtitle :title="'Вернём ковру былую яркость'"
        :subtitle="'Несколько простых этапов для профессиональной стирки Вашего ковра'" />
      <div class="steps">
        <div v-for="(step, index) in steps" :key="index" class="step">
          <div class="step-number">{{ index + 1 }}</div>
          <h3 class="step-title">{{ step.title }}</h3>
          <p class="step-text">{{ step.text }}</p>
        </div>
      </div>

      <Button />

      <div class="text">
        Перезвоним, произведём расчёт <strong>со скидкой 20%</strong> и ответим
        на все вопросы
      </div>
    </section>

    <Slider />

    <section id="block4">
      <div class="title"></div>
      <div class="description"></div>
      <TitleSubtitle :title="'Сертифицированные чистящие средства'"
        :subtitle="'100% безопасно для детей, взрослых и домашних животных'" />
      <div class="image">
        <img
          src="https://optim.tildacdn.com/tild3465-3738-4131-b831-326362306631/-/format/webp/himchistka_krasnodar.jpg.webp"
          alt="Чистящие средства">
      </div>

      <Button style="margin-top: 60px;" />

      <div class="text">Перезвоним, произведём расчёт <strong>со скидкой 20%</strong> и ответим на все вопросы</div>
    </section>

    <section id="block5">
      <TitleSubtitle :title="'Стоимость стирки ковров'" :subtitle="'Закажите сейчас со скидкой 20%'" />
      <div class="cards">
        <div class="card">
          <div class="card-img"><img
              src="https://optim.tildacdn.com/tild6236-6664-4736-b834-313966646535/-/resize/372x/-/format/webp/Sintetika_kover.jpg.webp"
              alt="Пример работы"></div>
          <div class="card-title">Шерстяные и синтетические ковры</div>
          <div class="card-price">455 руб./м2</div>
          <div class="card-services">вывоз, стирка и доставка</div>
          <div class="card-price-discount">570 руб./м2</div>
          <Button :text="'Рассчитать стоимость'" />
        </div>
        <div class="line"></div>
        <div class="card">
          <div class="card-img"><img
              src="https://optim.tildacdn.com/tild3963-3936-4264-b861-666234663866/-/resize/372x/-/format/webp/Viskoz_kover.jpg.webp"
              alt="Пример работы"></div>
          <div class="card-title">Вискозные <br> ковры</div>
          <div class="card-price">495 руб./м2</div>
          <div class="card-services">вывоз, стирка и доставка</div>
          <div class="card-price-discount">620 руб./м2</div>
          <Button :text="'Рассчитать стоимость'" />
        </div>
        <div class="line"></div>
        <div class="card">
          <div class="card-img"><img
              src="https://optim.tildacdn.com/tild3236-3464-4631-b039-626435356462/-/resize/372x/-/format/webp/Shelk_kover.jpg.webp"
              alt="Пример работы"></div>
          <div class="card-title">Шёлковые <br> ковры</div>
          <div class="card-price">990 руб./м2</div>
          <div class="card-services">вывоз, стирка и доставка</div>
          <div class="card-price-discount">1240 руб./м2</div>
          <Button :text="'Рассчитать стоимость'" />
        </div>
      </div>
      <div class="deal">
        <div class="text">Предоставим дополнительную скидку на большой заказ</div>
        <div class="outer"><svg role="presentation" version="1.1" viewBox="0 0 1200 31.7" width="1200px" height="40px">
            <g>
              <polygon points="40,31.7 40,4 0,4 0,0 44,0 44,22.3 67.2,0 1200,0 1200,4 68.8,4 "></polygon>
            </g>
          </svg>
        </div>
        <div class="author">
          <div class="ava"><img src="/Images/Main/ava.png" alt=""></div>
          <div class="cont">
            <div class="name">Хамхоев Адам</div>
            <div class="post">Владелец</div>
          </div>
        </div>
      </div>
    </section>

    <section id="block6">
      <ModalWindow />
    </section>

    <section id="block7">
      <TitleSubtitle :title="'Дополнительные услуги'" :subtitle="'Качественные услуги от специалистов по коврам'" />

      <Slider2 />
    </section>

    <section id="block8">
      <TitleSubtitle :title="'Наши клиенты'"
        :subtitle="'Тысячи положительных отзывов от организаций и жителей Краснодара'" />

      <div>
        <img v-for="value in ourClients" :src="value" alt="">
      </div>
    </section>

    <section id="block9">
      <div class="overlay">
        <div class="title">Нас благодарят🧡</div>

        <div class="cards">
          <div class="card" v-for="(review, index) in reviews" :key="index">
            <div class="author">
              <img :src="review.image" alt="Фото" class="avatar" />
              <div>
                <h3 class="name">{{ review.name }}</h3>
                <p class="role">{{ review.role }}</p>
              </div>
            </div>
            <p class="text">{{ review.text }}</p>
          </div>
        </div>
      </div>
    </section>

    <section id="block10">
      <div class="qr-code"></div>
      <div>
        <div class="title">Остались вопросы?</div>

        <p>Звоните:</p>
        <a href="tel:8-938-488-33-11">8-938-488-33-11</a>
        <br>
        <a href="tel:8-861-292-22-33">8-861-292-22-33</a>
        <br><br><br>
        <p>Краснодар, Дмитрия Благоева 29</p>
        <p>с 08:00 до 20:00 без выходных</p>
        <br><br>
        <p>ИП Кондратьев С. А.</p>
        <p>ИНН 650115051521</p>
        <p>ОГРН 320237500345968</p>
        <br><br>
        <Button />
      </div>
    </section>
  </main>
</template>

<script>
import PhoneInput from "./PhoneInput.vue";
import { ref } from "vue";
import Slider from "./Slider.vue";
import Button from "./Button.vue";
import ModalWindow from "./ModalWindow.vue";
import Slider2 from "./Slider2.vue";
import TitleSubtitle from "./TitleSubtitle.vue";

export default {
  components: {
    PhoneInput,
    Button,
    Slider,
    ModalWindow,
    Slider2,
    TitleSubtitle
  },
  setup() {
    const phone = ref("");
    const isFormValid = ref(false);
    const phoneInput = ref(null);

    const handleValidation = (validation) => {
      isFormValid.value = validation.isValid;
      // console.log("Валидация:", validation);
    };

    const submitForm = () => {
      if (!phoneInput.value.getFormattedNumber()) {
        alert("Пожалуйста, введите номер телефона");
        return;
      }

      if (!isFormValid.value) {
        alert("Пожалуйста, введите корректный номер телефона");
        return;
      }

      const formattedNumber = phoneInput.value
        ? phoneInput.value.getFormattedNumber()
        : phone.value;

      alert(
        `Спасибо за заявку! Мы перезвоним вам по номеру: ${formattedNumber}`
      );

      phone.value = "";
      if (phoneInput.value) {
        phoneInput.value.clear();
      }
    };

    const lists = [
      {
        src: "https://static.tildacdn.com/lib/tildaicon/34636363-6538-4037-a638-313766633963/Tilda_Icons_42_restaurant_burger.svg",
        text: "Пятна от еды и напитков"
      },
      {
        src: "https://static.tildacdn.com/lib/tildaicon/61366638-6366-4933-a565-363231303030/34Vet_dog.svg",
        text: "Следы животных, мочу и шерсть"
      },
      {
        src: "https://static.tildacdn.com/lib/tildaicon/38623462-6232-4265-b330-393937383535/Tilda_Icons_28_tattoo_creme.svg",
        text: "Косметика, йод, зелёнка"
      },
      {
        src: "https://static.tildacdn.com/lib/tildaicon/36306230-3932-4561-b061-613363336234/Tilda_Icons_28_tattoo_draw.svg",
        text: "Краска и фломастеры"
      },
      {
        src: "https://static.tildacdn.com/lib/tildaicon/36636134-6565-4333-a533-636239336239/kideducate_kid.svg",
        text: "Пластилин и слаймы"
      },
      {
        src: "https://static.tildacdn.com/lib/tildaicon/36376461-3233-4135-a437-366235663364/Tilda_Icons_38_Cleaning_company_clean.svg",
        text: "Грязь, плесень, гниль"
      }
    ]

    const steps = [
      {
        title: "Вы оставляете заявку или звоните",
        text: "Мы за 1 минуту рассчитаем стоимость и определим время вывоза",
      },
      {
        title: "Мы приезжаем за ковром",
        text: "Водитель приедет за ковром в удобное для Вас время",
      },
      {
        title: "Технолог замерит и осмотрит ковёр",
        text: "Ещё до стирки ковёр замерит и осмотрит технолог",
      },
      {
        title: "12 этапов стирки Вашего ковра",
        text: "Осмотрим, почистим, постираем, прополощем, высушим, вычешем...",
      },
      {
        title: "Высушим до 100%",
        text: "Сушим ковёр в специальной сушильной камере до 100%",
      },
      {
        title: "Упаковываем и доставляем",
        text: "Через 3–6 дней вы получите чистый, сухой, упакованный ковёр",
      },
    ];

    const ourClients = [
      "https://optim.tildacdn.com/tild6262-3939-4231-b032-633336653638/-/resize/180x/-/format/webp/stirka_sanatorii.png.webp",
      "https://optim.tildacdn.com/tild6435-6462-4336-b632-346231356266/-/resize/180x/-/format/webp/stirka_restoran.jpg.webp",
      "https://optim.tildacdn.com/tild6136-3234-4665-b230-383032366631/-/resize/180x/-/format/webp/stirka_kafe.jpg.webp",
      "https://optim.tildacdn.com/tild3762-6630-4435-b732-373233316466/-/resize/180x/-/format/webp/stirka_sad.jpg.webp",
      "https://optim.tildacdn.com/tild3938-3361-4664-b031-653265336265/-/resize/180x/-/format/webp/stirka_fso.jpg.webp",
      "https://optim.tildacdn.com/tild3635-3466-4562-b035-303063666431/-/resize/180x/-/format/webp/stirka_fsb.jpg.webp",
      "https://optim.tildacdn.com/tild6663-3564-4335-a430-376561363833/-/resize/180x/-/format/webp/stirka_bank.jpg.webp",
      "https://optim.tildacdn.com/tild3033-6137-4565-b237-316637383338/-/resize/180x/-/format/webp/stirka_ris.jpg.webp",
      "https://optim.tildacdn.com/tild3162-6334-4538-b833-373863643033/-/resize/180x/-/format/webp/stirka_pizza.jpg.webp",
      "https://optim.tildacdn.com/tild3038-3930-4964-a165-643838326430/-/resize/180x/-/format/webp/stirka_dacha.jpg.webp"
    ]

    const reviews = [
      {
        image: "https://static.tildacdn.com/tild6435-6438-4765-b839-316536373264/stirka_kovra_3.jpg",
        name: "Арут Каракеян",
        role: "Отец и предприниматель",
        text: "Отдал в химчистку старый (27-летний) ковёр, а забрал новый. Все пятна ушли, ворс поднялся. Буду обращаться ещё."
      },
      {
        image: "https://static.tildacdn.com/tild6638-6230-4463-b561-623534303763/stirka_kovra_2.jpg",
        name: "Мария Семёхина",
        role: "Руководитель детского сада \"ЁЖ\"",
        text: "Уже трижды обращались за химчисткой ковров и трижды остались довольны. Ковры не пахнут и идеально чистые. Очень рекомендую!"
      },
      {
        image: "https://static.tildacdn.com/tild3339-6461-4364-a539-343733613834/stirka_kovra_1.jpg",
        name: "Григорий и Светлана",
        role: "Молодая семья",
        text: "Отдали в стирку сразу шесть ковров и уже через 4 дня получили обратно. Трудно поверить, что их можно было так отстирать. Спасибо."
      }
    ];


    return {
      phone,
      isFormValid,
      phoneInput,
      handleValidation,
      submitForm,
      steps,
      lists,
      ourClients,
      reviews
    };
  },
};
</script>

<style scoped>
#block1 {
  background-image: url(/Images/Main/Stirka_kovrov.jpg);
  position: relative;
  background-size: cover;
  background-position: center;
  padding: 40px 20px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

#block1 .title {
  color: var(--primary-color);
  font-weight: 500;
  font-size: 62px;
  line-height: 60px;
  margin-bottom: 20px;
}

#block1 .description {
  color: #fff;
  font-size: 52px;
  font-weight: 500;
  margin-bottom: 30px;
}

#block1 .form {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
  position: relative;
  z-index: 10;
}

#block1 .form input[type="button"] {
  padding: 17px 40px;
  background: var(--primary-color);
  color: white;
  border: 1px solid var(--primary-color);
  height: 56px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 700;
  text-transform: uppercase;
  transition: 0.5s;
}

#block1 .form input[type="button"]:hover:not(.button-disabled) {
  cursor: pointer;
  background-color: transparent;
  color: var(--primary-color);
}

#block1 .button-disabled {
  background: #ccc !important;
  cursor: not-allowed !important;
}

#block1 .text {
  color: white;
  font-size: 18px;
  font-weight: 300;
  position: relative;
  z-index: 5;
}

#block1::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.75);
  z-index: 1;
}

#block1>* {
  position: relative;
  z-index: 2;
}

#block2 {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 135px 0;
  background-color: #f0f0f0;
}

#block2 .video {
  padding-top: 30px;
  width: 1000px;
}

#block2 .video video {
  width: 100%;
}

#block2 .list {
  display: grid;
  width: 1000px;
  grid-template-columns: repeat(2, 3fr);
  gap: 50px;
  padding: 15px;
}

#block2 .list>div {
  display: flex;
  align-items: center;
  font-weight: 300;
  font-size: 22px;
  line-height: 1.35;
}

#block2 .list img {
  width: 40px;
  height: 40px;
  margin-right: 15px;
}

#block2 .text {
  margin-top: 15px;
  font-size: 16px;
  line-height: 1.55;
  font-weight: 300;
}

#block3 {
  padding: 135px 0;
  text-align: center;
  background: #fff;
}

#block3 .steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 50px;
  max-width: 1100px;
  margin: 60px auto;
  margin-top: 100px;
}

#block3 .step {
  position: relative;
  padding: 20px;
}

#block3 .step-number {
  position: absolute;
  top: -65%;
  left: 50%;
  transform: translateX(-50%);
  font-size: 200px;
  font-weight: 700;
  color: rgba(230, 230, 230, .7);
  opacity: .6;
  user-select: none;
  z-index: 1;
  font-family: sans-serif;
}

#block3 .step-title {
  font-weight: 600;
  font-size: 20px;
  margin-bottom: 10px;
  position: relative;
  z-index: 2;
}

#block3 .step-text {
  font-size: 15px;
  color: #666;
  line-height: 1.4;
  position: relative;
  z-index: 2;
}

#block3 .text {
  margin-top: 20px;
  font-size: 16px;
  color: #444;
}

#block4 {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 135px 0;
  background-color: #f0f0f0;
}

#block4 .image {
  width: 100%;
  padding: 40px;
}

#block4 .image img {
  border-radius: 30px;
  width: 100%;
  height: 700px;
  object-fit: cover;
}

#block4 .text {
  margin-top: 15px;
  text-align: center;
}

#block5 {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 135px 0;
}

#block5 .cards {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 1200px;
  position: relative;
  margin-top: 30px;
}

#block5 .card {
  width: 340px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

#block5 .card:hover .card-img img {
  scale: 1.04;
}

#block5 .card-img {
  width: 100%;
  height: 186px;
  overflow: hidden;
}

#block5 .card-img img {
  width: 100%;
  object-fit: cover;
  transition: 0.5s;
}

#block5 .card-title {
  font-size: 24px;
  line-height: 1.35;
  font-weight: 600;
  margin-top: 25px;
}

#block5 .card-price,
#block5 .card-services,
#block5 .card-price-discount {
  font-size: 22px;
  line-height: 1.55;
  font-weight: 300;
}

#block5 .card-price-discount {
  margin-bottom: 30px;
  text-decoration: line-through;
}

#block5 .line {
  width: 1px;
  background-color: #d4d4d4;
  height: -webkit-fill-available;
}

#block5 .deal {
  width: 1050px;
  overflow: hidden;
  margin-top: 100px;
}

#block5 .deal .text {
  text-align: center;
  font-size: 36px;
  font-weight: 400;
  padding: 15px 0;
  border-top: 4px solid black;
}

#block5 .deal .author {
  display: flex;
  align-items: center;
  margin-top: 10px;
}

#block5 .deal .ava {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
}

#block5 .deal .ava img {
  width: 100%;
}

#block5 .deal .cont {
  margin-left: 15px;
}

#block5 .deal .name {
  font-size: 18px;
  font-weight: 600;
  line-height: 22px;
}

#block5 .deal .post {
  font-size: 16px;
  line-height: 20px;
}

#block6 {
  display: flex;
  justify-content: center;
  width: 100%;
}

#block7 {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #e8e8e8;
  padding: 135px 0;
}

#block8 {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 135px 0;
}

#block8 :last-child {
  display: grid;
  justify-content: center;
  align-items: center;
  grid-template-columns: repeat(5, 1fr);
  width: 1200px;
  row-gap: 30px;
  margin-top: 40px;
}

#block8 :last-child img {
  max-width: 150px;
  margin: auto;
}

#block9 {
  width: 100%;
  height: 100vh;
  background-image: url('https://optim.tildacdn.com/tild6663-6137-4531-b862-393035646432/-/format/webp/stirka_kovrov_himchi.jpg.webp');
  background-size: cover;
  position: relative;
}

#block9::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  z-index: 1;
}

#block9 .overlay {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 4;
}

#block9 .title {
  font-size: 46px;
  color: #fff;
  line-height: 1.23;
  font-weight: 600;
  text-align: center;
}

#block9 .cards {
  display: flex;
  justify-content: center;
  gap: 40px;
  margin-top: 50px;
}

#block9 .card {
  background: #fff;
  border-radius: 5px;
  padding: 40px;
  width: 360px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
}

#block9 .author {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
}

#block9 .avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 12px;
}

#block9 .name {
  font-weight: 600;
  margin: 0;
  font-size: 16px;
  line-height: 1.35;
}

#block9 .role {
  font-size: 14px;
  color: #757575;
  line-height: 1.55;
  margin: 0;
}

#block9 .text {
  font-size: 14px;
  line-height: 1.55;
  font-weight: 300;
}

#block10 {
  padding-top: 135px;
  display: flex;
  align-items: center;
  justify-content: center;
}

#block10 .qr-code {
  width: 460px;
  height: 460px;
  background-image: url('https://static.tildacdn.com/tild6335-6565-4439-b064-393737376262/krasnodar_kontakt.png');
  background-size: 460px;
  box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.2);
  margin-right: 140px;
}

#block10 .title {
  text-transform: uppercase;
  font-size: 42px;
  line-height: 1.23;
  font-weight: 600;
  margin-bottom: 34px;
}

#block10 p {
  font-size: 18px;
  line-height: 1.55;
  font-weight: 300;
}

#block10 a {
  font-size: 28px;
  box-shadow: inset 0px -1px 0px 0px #ff3503;
  border-bottom: 0px solid #ff3503;
  font-weight: 300;
  color: black;
  text-decoration: none;
}

strong {
  font-weight: 700;
}

@media (max-width: 1200px) {
  #block2 .video,
  #block2 .list,
  #block5 .cards,
  #block5 .deal,
  #block8 :last-child {
    width: 100%;
    max-width: 95%;
  }

  #block5 .cards {
    flex-direction: column;
    gap: 40px;
  }

  #block5 .line {
    display: none;
  }

  #block5 .card {
    width: 100%;
    max-width: 500px;
  }

  #block8 :last-child {
    grid-template-columns: repeat(3, 1fr);
  }

  #block9 {
    height: 1138px;
  }

  #block9 .overlay {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  #block9 .cards {
    flex-direction: column;
    align-items: center;
  }

  #block9 .card {
    width: 90%;
    max-width: 400px;
  }

  #block10 {
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: 60px 20px;
  }

  #block10 .qr-code {
    margin-right: 0;
    margin-bottom: 30px;
  }
}

@media (max-width: 768px) {
  #block1 .title {
    font-size: 42px;
    line-height: 48px;
  }

  #block1 .description {
    font-size: 32px;
    line-height: 38px;
  }

  #block1 .form {
    flex-direction: column;
    align-items: center;
    gap: 15px;
  }

  #block1 .form input[type="button"] {
    width: 100%;
    max-width: 300px;
  }

  #block1 .text {
    font-size: 16px;
  }

  #block2 {
    padding: 60px 0;
  }

  #block2 .list {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  #block2 .list div {
    font-size: 18px;
  }

  #block2 .text {
    padding: 0 5px;
  }
  
  #block3 {
    padding: 60px 0;
  }

  #block3 .steps {
    grid-template-columns: 1fr;
    margin: 40px auto;
  }

  #block3 .step-number {
    font-size: 100px;
    top: -50%;
  }

  
  #block4 {
    padding: 60px 0;
  }

  #block4 .image {
    padding: 20px;
  }

  #block4 .image img {
    height: 400px;
  }
  
  #block4 .text {
    padding: 0 5px;
  }

  #block5 {
    padding: 60px 0;
  }

  #block5 .deal .text {
    font-size: 24px;
  }

  #block7 {
    padding: 60px 0;
  }

  #block8 {
    padding: 60px 0;
  }

  #block8 :last-child {
    grid-template-columns: repeat(2, 1fr);
  }

  #block9 {
    padding: 60px 20px;
  }

  #block9 .title {
    font-size: 36px;
  }

  #block9 .cards {
    margin-top: 30px;
    gap: 30px;
  }

  #block10 .qr-code {
    width: 300px;
    height: 300px;
    background-size: 300px;
  }

  #block10 .title {
    font-size: 32px;
  }

  #block10 a {
    font-size: 24px;
  }
}

@media (max-width: 480px) {
  #block1 {
    padding: 20px;
  }

  #block1 .title {
    font-size: 32px;
    line-height: 38px;
  }

  #block1 .description {
    font-size: 24px;
    line-height: 30px;
  }

  #block1 .text {
    font-size: 14px;
  }

  #block2 .list div {
    font-size: 16px;
  }

  #block2 .list img {
    width: 30px;
    height: 30px;
  }

  #block3 .step-title {
    font-size: 18px;
  }

  #block3 .step-text {
    font-size: 14px;
  }

  #block4 .image img {
    height: 300px;
  }

  #block5 .card-title {
    font-size: 20px;
  }

  #block5 .card-price,
  #block5 .card-services,
  #block5 .card-price-discount {
    font-size: 18px;
  }

  #block9 .title {
    font-size: 28px;
  }

  #block9 .overlay {
    width: 90%;
  }

  #block9 .card {
    padding: 20px;
    width: 100%;
  }

  #block10 .title {
    font-size: 28px;
  }

  #block10 p {
    font-size: 16px;
  }

  #block10 a {
    font-size: 20px;
  }
}
</style>