<script setup>
import CardItem from "./CardItem.vue";

const cards = [
  {
    name: "factory",
    width: 37,
    height: 37,
    title: "Поиск производителей по\u00A0товару",
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do\u00A0eiusmod incididunt\u00A0ut.",
  },
  {
    name: "mechanism",
    width: 35,
    height: 37,
    title: "Поиск конкретного производителя",
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do\u00A0eiusmod incididunt\u00A0ut.",
  },
  {
    name: "delivery",
    width: 49,
    height: 29,
    classImg: "possibilities-card__img--wide",
    title: "Доставка образцов товаров",
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do\u00A0eiusmod incididunt\u00A0ut.",
  },
];
</script>

<template>
  <section class="possibilities container">
    <CardItem
      v-for="card in cards"
      :key="card.name"
      :src="`/icons/${card.name}.svg`"
      :class-img="card.classImg"
      classMod="possibilities"
      :width="card.width"
      :height="card.height"
      :title="card.title"
      :text="card.text"
    />
  </section>
</template>

<style>
.possibilities {
  display: flex;
  flex-direction: column;
  gap: 24px;

  padding: 24px 27px 32px 32px;
  margin-block-end: 64px;

  border-radius: var(--border-radius-base);
  background-color: var(--color-primary-alt);
  filter: var(--box-shadow-base);
}

.possibilities-card {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.possibilities-card__img-box {
  display: grid;
  place-content: center;

  width: 68px;
  aspect-ratio: 1;

  background-color: var(--color-light);
  border-radius: 50%;
}

.possibilities-card__title {
  font: var(--font-heading-small);
  color: var(--color-text-heading);
  margin-block-end: 1.2rem;
}

@media (min-width: 768px) {
  .possibilities {
    gap: 16px;

    padding: initial;
    margin-block-end: 8.8rem;

    filter: initial;
}

.possibilities-card {
  flex-direction: row;
  gap: 32px;

  padding: 32px 140px 40px 32px;

  border-radius: var(--border-radius-base);
  background-color: var(--color-primary-alt);
  filter: var(--box-shadow-base);
}

.possibilities-card__img-box {
  width: 92px;
}

.possibilities-card__img {
  width: auto;
  height: 50px;
}

.possibilities-card__img--wide {
  width: 66px;
  height: 39px;
}

.possibilities-card__title {
  margin-block-end: 2rem;
}
}

@media (min-width: 1440px) {
  .possibilities {
    flex-flow: row wrap;
    justify-content: space-between;

    padding: 40px 80px 56px 16px;
    margin-block-end: 10rem;

    filter: var(--box-shadow-base);
}

.possibilities-card {
  flex-direction: column;
  gap: 24px;
  flex: 1 1 370px;

  padding: 0 0 16px 64px;
  border-radius: initial;
  filter: initial;

  &:not(:nth-child(3n + 1)) {
    background: linear-gradient(90deg, #D7D7DD 0 0) 0 0 / 1px 100% no-repeat;
  }
}

.possibilities-card__title {
  margin-block-end: 1.6rem;
}
}
</style>
