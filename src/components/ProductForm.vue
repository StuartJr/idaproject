<template>
  <div class="form">
    <div class="form__wrapper">
      <div class="form__container">
        <div :class="['form__item', { error: isTitleError }]">
          <label for="title" class="form__label"
            >Наименование товара <span class="form__circle"></span
          ></label>
          <input
            id="title"
            type="text"
            class="form__input"
            placeholder="Введите наименование товара"
            v-model="title"
          />
          <p class="form__error">Поле является обязательным</p>
        </div>
        <div :class="['form__item', { error: isDescError }]">
          <label for="desc" class="form__label"
            >Описание товара <span class="form__circle"></span
          ></label>
          <textarea
            id="desc"
            type="text"
            class="form__input form__input--textarea"
            placeholder="Введите описание товара"
            v-model="desc"
          ></textarea>
          <p class="form__error">Поле является обязательным</p>
        </div>
        <div :class="['form__item', { error: isImgError }]">
          <label for="img" class="form__label"
            >Ссылка на изображение товара <span class="form__circle"></span
          ></label>
          <input
            id="img"
            type="text"
            class="form__input"
            placeholder="Введите ссылку"
            v-model="img"
          />
          <p class="form__error">Поле является обязательным</p>
        </div>
        <div :class="['form__item', { error: isPriceError }]">
          <label for="price" class="form__label"
            >Цена товара <span class="form__circle"></span
          ></label>
          <input
            id="price"
            type="text"
            class="form__input"
            placeholder="Введите цену"
            v-model="price"
          />
          <p class="form__error">Поле является обязательным</p>
        </div>
      </div>
      <button @click="addCard()" class="form__add" :disabled="isDisabledButton">
        Добавить товар
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "product-form",
  data() {
    return {
      title: "",
      desc: "",
      img: "",
      price: "",
      isTitleError: false,
      isDescError: false,
      isImgError: false,
      isPriceError: false,
    };
  },
  computed: {
    isDisabledButton() {
      return !(
        this.title.length >= 1 &&
        this.desc.length >= 1 &&
        this.img.length >= 1 &&
        this.price.length >= 1
      );
    },
  },
  methods: {
    clearInputs() {
      this.title = "";
      this.desc = "";
      this.img = "";
      this.price = "";

      this.$nextTick(() => {
        this.isTitleError = false;
        this.isDescError = false;
        this.isImgError = false;
        this.isPriceError = false;
      });
    },
    addCard() {
      const object = {
        id: new Date().getTime(),
        img: this.img.trim(),
        title: this.title.trim(),
        desc: this.desc.trim(),
        price: this.price.trim(),
      };

      this.$emit("addCardHandler", object);
      this.clearInputs();
    },
  },
  watch: {
    title() {
      this.isTitleError = this.title.length === 0;
    },
    desc() {
      this.isDescError = this.desc.length === 0;
    },
    img() {
      this.isImgError = this.img.length === 0;
    },
    price() {
      this.price = this.price.replace(/[a-zA-Zа-яА-Я]/g, "");
      this.price = this.price
        .replace(/[^0-9.]/g, "")
        .replace(/\B(?=(\d{3})+(?!\d))/g, " ");
      this.isPriceError = this.price.length === 0;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./../style/_variable";
.form {
  width: 100%;
  max-width: 348px;
  padding-right: 16px;

  &__wrapper {
    position: sticky;
    top: 24px;
    background: $color-light-grey;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
      0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    padding: 24px;
  }
  &__item {
    width: 100%;
    display: flex;
    flex-direction: column;
    position: relative;

    &:not(:last-child) {
      padding-bottom: 16px;
    }

    &.error {
      .form__input {
        border: 1px solid $color-red;
      }
      .form__error {
        display: block;
      }
    }
  }
  &__label {
    display: inline-flex;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: $color-dark;
    margin-bottom: 4px;
  }
  &__circle {
    width: 4px;
    height: 100%;
    position: relative;

    &:after {
      content: "";
      position: absolute;
      right: 0;
      top: 0;
      width: 4px;
      height: 4px;
      border-radius: 50%;
      background-color: $color-red;
    }
  }
  &__input {
    background-color: $color-light-grey;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 16px 11px;
    font-size: 12px;
    line-height: 15px;
    color: $color-black;

    &::placeholder {
      font-size: 12px;
      line-height: 15px;
      color: $color-grey;
    }

    &--textarea {
      resize: none;
      height: 125px;
    }
  }
  &__error {
    display: none;
    position: absolute;
    bottom: 2px;
    font-size: 8px;
    line-height: 10px;
    letter-spacing: -0.02em;
    color: $color-red;
  }
  &__add {
    margin-top: 24px;
    width: 100%;
    height: 36px;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    background-color: $color-green;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Inter";
    font-size: 12px;
    line-height: 15px;
    color: $color-white;
    transition: all 0.3s ease;

    &:disabled {
      color: $color-grey;
      background-color: $color-disabled;
      cursor: default;
    }
  }
}
</style>
