<script setup>
import PictureOptimized from "./PictureOptimized.vue";
</script>

<template>
  <section class="intro container">
    <div class="intro__box">
      <h1 class="intro__title">Поставщик Дальнего Востока</h1>
      <p class="intro__text">
        Наши клиенты получают полный спектр услуг по&nbsp;работе с&nbsp;Китаем. Начиная
        с&nbsp;подбора производителя заканчивая доставкой товара до&nbsp;двери.<span
          class="intro__hide"
        >
          Настолько прозрачных сделок с&nbsp;Китаем вы&nbsp;еще не&nbsp;осуществляли.</span
        >
      </p>
      <a class="intro__link" href="javascript: void(0)">Узнать больше</a>
    </div>
    <PictureOptimized
      class="intro__picture"
      name="adir-Cargo-Insurance"
      alt="Грузовики на дороге"
      dir="/images/intro/"
      :width-mobile="345"
      :height-mobile="253"
      :width-tablet="690"
      :height-tablet="314"
      :width-desktop="580"
      :height-desktop="461"
    />
  </section>
</template>

<style>
.intro {
  padding-block-start: 75px;
  margin-block-end: 58px;

  color: var(--color-on-surface);
}

.intro__title {
  margin-block-end: 32px;

  font: var(--font-heading);
  color: var(--color-on-surface);
}

.intro__box {
  margin-block-end: 40px;
}

.intro__hide {
  display: none;
}

.intro__link {
  display: inline-block;

  padding-block-end: 5px;
  margin-block-start: 32px;

  font-weight: 700;
  line-height: 150%;
  text-decoration: none;
  color: inherit;

  background: linear-gradient(var(--color-secondary) 0 0) 0 100% / calc(100% / var(--g, 1)) 3px
    no-repeat;
  transition: 0.3s;

  &:hover {
    --g: 2;
  }
}

.intro__picture {
  border-radius: var(--border-radius-base);
}

@media (min-width: 768px) {
  .intro {
    padding-block-start: 80px;
    margin-block-end: 41px;

    color: var(--color-text-body);
    border-image: linear-gradient(90deg, #0000 0 calc(100vw - 39px - 12%), var(--color-primary) 0) fill 0 // 0 100vw 0 0;
  }

  .intro__title {
    margin-block-end: 40px;
    color: var(--color-text-heading);
  }

  .intro__box {
    max-inline-size: 75%;
  }

  .intro__hide {
    display: inline;
  }

  .intro__link {
    margin-block-start: 61px;
    color: var(--color-text-heading);
  }
}

@media (min-width: 1440px) {
  .intro {
    display: flex;
    align-items: center;
    gap: 80px;

    padding-block-start: 109px;
    margin-block-end: 67px;
  }

  .intro__box,
  .intro__picture {
    flex: 1;
  }

  .intro__box {
    margin-block-end: 0;
  }

  .intro__link {
    margin-block-start: 40px;
  }
}
</style>
