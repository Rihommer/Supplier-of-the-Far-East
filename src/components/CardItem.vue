<script setup>
defineProps({
  src: { type: String, required: true },
  classImg: { type: String, default: "" },
  classMod: { type: String, default: "" },
  alt: { type: String, default: "" },
  width: { type: Number, default: undefined },
  height: { type: Number, default: undefined },
  ariaHidden: { type: Boolean, default: true },
  title: { type: String, default: "" },
  text: { type: String, default: "" },
});
</script>

<template>
  <div :class="`${classMod}-card`">
    <div :class="`${classMod}-card__img-box`">
      <img :class="[`${classMod}-card__img`, classImg]" :src :alt :width :height :aria-hidden />
    </div>
    <div :class="`${classMod}-card__box`">
      <p :class="`${classMod}-card__title`">{{ title }}</p>
      <p :class="`${classMod}-card__text`">{{ text }}</p>
      <slot name="social">
        <div :class="`${classMod}-card__social`"></div>
      </slot>
    </div>
  </div>
</template>