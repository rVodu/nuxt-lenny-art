<template>
  <form class="subscribe-form" @submit.prevent="onSubmit">
    <h4 class="subscribe-form__title">Подпишись и будь в курсе происходящего</h4>

    <div class="subscribe-form__wrapper">
      <div class="subscribe-form__field-wrapper">
        <input class="subscribe-form__input" type="email" placeholder="Email" v-model="email" />
        <span v-if="submitCount && (!email || !emailIsValid)" class="subscribe-form__error field-error">
          {{
            email && !emailIsValid
              ? "Email указан неверно"
              : "Это поле обязательно"
          }}
        </span>

      </div>
      <button type="submit" class="subscribe-form__submit">
        Подписаться
      </button>
    </div>

    <label class="subscribe-form__check check">
      <input class="check__input" type="checkbox" v-model="agreement" :true-value="1" :false-value="0" />

      <span class="check__mark"></span>
      <span class="check__label check__label--s">
        Согласен на обработку персональных данных </span>
    </label>

    <span v-if="submitCount && !agreement" class="subscribe-form__error field-error">
      Это поле обязательно
    </span>

  </form>
</template>

<script setup>
  const email = ref("");
  const agreement = ref(0);

  const submitCount = ref(0);

  const emailIsValid = computed(() => {
    return /^[-\w.]+@([A-z0-9][-A-z0-9]+\.)+[A-z]{2,6}$/.test(email.value);
  });

  const onSubmit = () => {
    submitCount.value += 1;
     if (!email.value || !emailIsValid.value || !agreement.value) return;

    console.log({ 
    email: email.value, 
    agreement: agreement.value 
  });
    alert("Подписка оформлена");
  };
</script>

<style lang="less">
.subscribe-form {
  width: 405px;
  max-width: 100%;
  display: flex;
  flex-direction: column;

  @media @bw370 {
    margin-left: 0;
    padding: 0;
  }

  &__title {
    margin: 0 0 25px;
    font-size: 16px;
    line-height: 22px;

    @media @bw500 {
      margin: 0 0 15px;
      font-weight: 400;
      font-size: 13px;
      line-height: 18px;
    }

    @media @bw370 {
      font-size: 13px;
      font-family: @font1;
    }
  }

  &__wrapper {
    display: flex;
    justify-content: space-between;
  }

  &__field-wrapper {
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    margin-bottom: 15px;

    @media @bw370 {
      width: 204px;
    }
  }

  &__input {
    box-sizing: border-box;
    padding: 0 25px;
    width: 100%;
    height: 49px;
    border: none;
    background-color: @white;
    font-size: 14px;
    line-height: 19px;
  }

  &__submit {
    width: 135px;
    height: 49px;
    border: none;
    text-align: center;
    background-color: @black;
    color: @white;

    @media @bw370 {
      width: 116px;
    }
  }

  &__error {
    margin: 5px 0 0;
  }
}
</style>