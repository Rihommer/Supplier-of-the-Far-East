<script setup>
import InputItem from "./InputItem.vue";
import { ref, computed, onMounted } from "vue";

const voteCount = ref(1107);
const selectedItem = ref(null);
const inputs = ref([
  {
    name: "area-work",
    id: "prodaction",
    title: "Я\u00A0работаю на\u00A0производстве",
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do\u00A0eiusmod tempor incididunt ut\u00A0labore et\u00A0dolore magna aliqua.",
  },
  {
    name: "area-work",
    id: "supply",
    title: "Я\u00A0поставляю товары",
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do\u00A0eiusmod tempor incididunt ut\u00A0labore et\u00A0dolore magna aliqua.",
  },
  {
    name: "area-work",
    id: "help-select",
    title: "Я\u00A0помогаю подобрать оборудование",
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do\u00A0eiusmod tempor incididunt ut\u00A0labore et\u00A0dolore magna aliqua.",
  },
]);

onMounted(() => {
  const savedVote = localStorage.getItem('userVote');
  if (savedVote) {
    selectedItem.value = savedVote;
  }

  const savedCount = localStorage.getItem('voteCount');
  if (savedCount) {
    voteCount.value = parseInt(savedCount);
  }
});

const handleUpdate = (id) => {
  if (localStorage.getItem('userVote')) {
    return;
  }

  selectedItem.value = id;
  localStorage.setItem('userVote', id);

  voteCount.value += 1;
  localStorage.setItem('voteCount', voteCount.value.toString());
};

// const fetchVoteCount = async () => {
//   try {
//     const response = await fetch('http://localhost:5173/api/votes/count');
//     if (response.ok) {
//       const data = await response.json();
//       voteCount.value = data.count;
//     }
//   } catch (error) {
//     console.error('Ошибка при загрузке данных:', error);
//   }
// };

// onMounted(async () => {
//   await fetchVoteCount();

//   const savedVote = localStorage.getItem('userVote');
//   if (savedVote) {
//     selectedItem.value = savedVote;
//   }
// });

// const handleUpdate = async (id) => {
//   if (localStorage.getItem('userVote')) {
//     return;
//   }

//   try {
//     const response = await fetch('http://localhost:5173/api/votes', {
//       method: 'POST',
//       headers: {
//         'Content-Type': 'application/json',
//       },
//       body: JSON.stringify({ optionId: id })
//     });

//     if (response.ok) {
//       selectedItem.value = id;
//       localStorage.setItem('userVote', id);

//       await fetchVoteCount();
//     } else {
//       console.error('Ошибка при отправке голоса');
//     }
//   } catch (error) {
//     console.error('Ошибка сети:', error);
//   }
// };

const getUsersWord = (count) => {
  const lastTwo = Math.abs(count) % 100;
  const lastOne = lastTwo % 10;

  if (lastTwo > 10 && lastTwo < 20) return 'пользователей';
  if (lastOne === 1) return 'пользователь';
  if (lastOne > 1 && lastOne < 5) return 'пользователя';
  return 'пользователей';
};

const formattedResult = computed(() => {
  const formattedNumber = new Intl.NumberFormat("ru-RU").format(voteCount.value);
  return {
    number: formattedNumber,
    text: getUsersWord(voteCount.value)
  };
});

const setInitialSelection = () => {
  const savedVote = localStorage.getItem('userVote');
  selectedItem.value = savedVote || inputs.value[0].id;
};

onMounted(() => {
  setInitialSelection();
  const savedCount = localStorage.getItem('voteCount');
  if (savedCount) voteCount.value = parseInt(savedCount);
});
</script>

<template>
  <section class="container survey" aria-labelledby="survey-title">
    <div class="survey__box">
      <h2 class="survey__title" id="survey-title">В&nbsp;какой сфере вы&nbsp;работаете?</h2>
      <p class="survey__text">
        Мы&nbsp;проводим опрос среди пользователей сайта, чтобы предоставить Вам информацию
        соответствующую сфере Вашей деятельности.
      </p>
      <div
        role="radiogroup"
        aria-labelledby="survey-title"
        >
        <InputItem
          v-for="input in inputs"
          v-model="selectedItem"
          :key="input.id"
          :name="input.name"
          :id="input.id"
          :title="input.title"
          :text="input.text"
          :tabindex="0"
          @update:modelValue="handleUpdate"
        />
      </div>
    </div>
    <div class="survey__result">
      <p class="survey__description">Проголосовало:</p>
      <p class="survey__value-box"><span class="survey__value">{{ formattedResult.number }}</span> {{ formattedResult.text }}</p>
    </div>
  </section>
</template>

<style>
.survey {
  margin-block-end: 6.4rem;
}

.survey__title {
  margin-block-end: 3.2rem;

  font: var(--font-heading);
  color: var(--color-text-heading);
}

.survey__text {
  display: none;
}

.survey__result {
  display: none;
}

@media(min-width: 768px) {
  .survey__text {
    display: block;
    margin-block-end: 4.8rem;
  }
}

@media(min-width: 1440px) {
  .survey {
    display: flex;
    gap: 140px;
  }

  .survey__box {
    inline-size: 687px;
  }

    .survey__text {
      margin-block-end: 4rem;
    }

  .survey__result {
    display: block;
    align-self: flex-start;

    padding-block-end: 1.9rem;
    margin-block-start: calc(113px + var(--font-size-heading));

    font: var(--font-heading-small);
    background: linear-gradient(0deg, var(--color-secondary) 0 3px, #0000 0 0);
  }

  .survey__description {
    margin-block-end: .8rem;
    color: var(--color-text-heading);
  }

  .survey__value {
    font-size: 5.4rem;
    line-height: 150%;
    color: var(--color-text-heading);
  }
}
</style>
