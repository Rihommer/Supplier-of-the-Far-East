<script setup>
const props = defineProps({
  name: { type: String, required: true },
  alt: { type: String, default: "" },
  dir: { type: String, default: "" },
  widthMobile: { type: Number, default: undefined },
  heightMobile: { type: Number, default: undefined },
  widthTablet: { type: Number, default: undefined },
  heightTablet: { type: Number, default: undefined },
  widthDesktop: { type: Number, default: undefined },
  heightDesktop: { type: Number, default: undefined },
});

const desktopAvif1x = new URL(`${props.dir}${props.name}-desktop-1x.avif`, import.meta.url).href;
const desktopAvif2x = new URL(`${props.dir}${props.name}-desktop-2x.avif`, import.meta.url).href;
const desktopWebp1x = new URL(`${props.dir}${props.name}-desktop-1x.webp`, import.meta.url).href;
const desktopWebp2x = new URL(`${props.dir}${props.name}-desktop-2x.webp`, import.meta.url).href;
const desktopJpg1x = new URL(`${props.dir}${props.name}-desktop-1x.jpg`, import.meta.url).href;
const desktopJpg2x = new URL(`${props.dir}${props.name}-desktop-2x.jpg`, import.meta.url).href;

const tabletAvif1x = new URL(`${props.dir}${props.name}-tablet-1x.avif`, import.meta.url).href;
const tabletAvif2x = new URL(`${props.dir}${props.name}-tablet-2x.avif`, import.meta.url).href;
const tabletWebp1x = new URL(`${props.dir}${props.name}-tablet-1x.webp`, import.meta.url).href;
const tabletWebp2x = new URL(`${props.dir}${props.name}-tablet-2x.webp`, import.meta.url).href;
const tabletJpg1x = new URL(`${props.dir}${props.name}-tablet-1x.jpg`, import.meta.url).href;
const tabletJpg2x = new URL(`${props.dir}${props.name}-tablet-2x.jpg`, import.meta.url).href;

const mobileAvif1x = new URL(`${props.dir}${props.name}-mobile-1x.avif`, import.meta.url).href;
const mobileAvif2x = new URL(`${props.dir}${props.name}-mobile-2x.avif`, import.meta.url).href;
const mobileWebp1x = new URL(`${props.dir}${props.name}-mobile-1x.webp`, import.meta.url).href;
const mobileWebp2x = new URL(`${props.dir}${props.name}-mobile-2x.webp`, import.meta.url).href;
const mobileJpg1x = new URL(`${props.dir}${props.name}-mobile-1x.jpg`, import.meta.url).href;
const mobileJpg2x = new URL(`${props.dir}${props.name}-mobile-2x.jpg`, import.meta.url).href;

const fallback = new URL(`${props.dir}${props.name}-desktop-2x.jpg`, import.meta.url).href;
</script>

<template>
  <picture>
    <source
      type="image/avif"
      media="(min-width: 1440px)"
      :srcset="`${desktopAvif1x} 1x, ${desktopAvif2x} 2x`"
      :width="widthDesktop"
      :height="heightDesktop"
    />
    <source
      type="image/webp"
      media="(min-width: 1440px)"
      :srcset="`${desktopWebp1x} 1x, ${desktopWebp2x} 2x`"
      :width="widthDesktop"
      :height="heightDesktop"
    />
    <source
      type="image/jpeg"
      media="(min-width: 1440px)"
      :srcset="`${desktopJpg1x} 1x, ${desktopJpg2x} 2x`"
      :width="widthDesktop"
      :height="heightDesktop"
    />

    <source
      type="image/avif"
      media="(min-width: 768px) and (max-width: 1439px)"
      :srcset="`${tabletAvif1x} 1x, ${tabletAvif2x} 2x`"
      :width="widthTablet"
      :height="heightTablet"
    />
    <source
      type="image/webp"
      media="(min-width: 768px) and (max-width: 1439px)"
      :srcset="`${tabletWebp1x} 1x, ${tabletWebp2x} 2x`"
      :width="widthTablet"
      :height="heightTablet"
    />
    <source
      type="image/jpeg"
      media="(min-width: 768px) and (max-width: 1439px)"
      :srcset="`${tabletJpg1x} 1x, ${tabletJpg2x} 2x`"
      :width="widthTablet"
      :height="heightTablet"
    />

    <source
      type="image/avif"
      media="(max-width: 767px)"
      :srcset="`${mobileAvif1x} 1x, ${mobileAvif2x} 2x`"
      :width="widthMobile"
      :height="heightMobile"
    />
    <source
      type="image/webp"
      media="(max-width: 767px)"
      :srcset="`${mobileWebp1x} 1x, ${mobileWebp2x} 2x`"
      :width="widthMobile"
      :height="heightMobile"
    />
    <source
      type="image/jpeg"
      media="(max-width: 767px)"
      :srcset="`${mobileJpg1x} 1x, ${mobileJpg2x} 2x`"
      :width="widthMobile"
      :height="heightMobile"
    />

    <img :src="fallback" :width="widthDesktop" :height="heightDesktop" :alt="alt" />
  </picture>
</template>
