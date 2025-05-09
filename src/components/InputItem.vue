<script setup>
import { computed } from "vue";

const props = defineProps({
  name: { type: String, required: true },
  id: { type: [String, Number], required: true },
  title: { type: String, default: "" },
  text: { type: String, default: "" },
  modelValue: { type: [String, Number], default: "" },
  tabindex: { type: Number, default: -1 }
});

const emit = defineEmits(["update:modelValue"]);
const isActive = computed(() => props.modelValue === props.id);
const selectItem = () => {
  emit("update:modelValue", props.id);
};

const handleKeyDown = (e) => {
  if ([" ", "Enter", "Spacebar"].includes(e.key)) {
    e.preventDefault();
    selectItem();
  }
};
</script>

<template>
  <div
    class="input-radio-item"
    role="radio"
    :aria-checked="isActive"
    :aria-labelledby="`label-${props.id}`"
    :tabindex="tabindex"
    @click="selectItem"
    @keydown="handleKeyDown"
  >
    <input
      class="input-radio-item__input"
      type="radio"
      :name="props.name"
      :id="props.id"
      :checked="isActive"
      @change="selectItem"
      tabindex="-1"
      aria-hidden="true"
    />
    <label
      class="input-radio-item__label"
      :for="props.id"
      :id="`label-${id}`">{{ props.title }}
    </label>
    <p class="input-radio-item__text">{{ props.text }}</p>
  </div>
</template>

<style>
.input-radio-item {
  padding: 24px 24px 32px 56px;

  background-color: var(--color-primary-alt);
  border-radius: calc(var(--border-radius-base) / 2);
  filter: var(--box-shadow-base);

  &:not(:last-child) {
    margin-block-end: 1rem;
  }

  &[aria-checked="true"] {
    box-shadow: 0 0 0 1px var(--color-primary);
  }
}

.input-radio-item__input {
  appearance: none;

  &:checked + .input-radio-item__label::after {
    display: block;
  }
}

.input-radio-item__label {
  position: relative;
  font: var(--font-heading-small);
  line-height: 150%;
  color: var(--color-text-heading);

  --outer-size: 2.4rem;
  --inner-size: 1rem;
  --indentation: 1.6rem;

  &::before {
    content: "";

    position: absolute;
    top: 0;
    left: calc(-1 * (var(--outer-size) + var(--indentation)));

    width: var(--outer-size);
    aspect-ratio: 1;

    border: 1px #cbcbcd solid;
    border-radius: 50%;
    box-shadow: inset 0 4px 4px rgba(0, 0, 0, 0.15);
  }

  &::after {
    content: "";
    display: none;

    position: absolute;
    top: calc((var(--outer-size) - var(--inner-size)) / 2);
    left: calc(-1 * (var(--indentation) + (var(--outer-size) + var(--inner-size)) / 2));

    width: var(--inner-size);
    aspect-ratio: 1;

    border-radius: 50%;
    background-color: var(--color-primary);
  }
}

.input-radio-item__text {
  margin-block-start: 1.6rem;
}

@media (min-width: 768px) {
  .input-radio-item {
    padding: 40px 125px 48px 96px;

    &:not(:last-child) {
      margin-block-end: 1.6rem;
    }
  }

  .input-radio-item__label {
    --indentation: 3.2rem;
  }

  .input-radio-item__text {
    margin-block-start: 2.4rem;
  }
}

@media (min-width: 1440px) {
  .input-radio-item {
    background: linear-gradient(
        343deg,
        var(--color-light) 0 16%,
        var(--color-primary-alt) 10% 0
      )
      no-repeat;
  }
}
</style>
