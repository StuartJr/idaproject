<template>
  <div class="main">
    <div class="container">
      <div class="main__header">
        <h2 class="main__title">Добавление товара</h2>
        <ProductSorting @setSelectHandler="setSelect" />
      </div>
      <div class="main__content">
        <ProductForm @addCardHandler="addCard" />
        <ProductList :list="list" @deleteItemHandler="deleteItem" />
      </div>
    </div>
  </div>
</template>

<script>
import ProductSorting from "@/components/ProductSorting.vue";
import ProductForm from "@/components/ProductForm.vue";
import ProductList from "@/components/ProductList.vue";

export default {
  name: "App",
  components: {
    ProductSorting,
    ProductForm,
    ProductList,
  },
  data() {
    return {
      list: [
        {
          id: new Date().getTime(),
          img: "https://images.wallpaperscraft.ru/image/single/fotoapparat_pirs_pesok_128809_1280x720.jpg",
          title: "Наименование товара",
          desc: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
      ],
      sorting: "default",
    };
  },
  methods: {
    //Добавление новой карточки в список
    addCard(item) {
      this.list = [...this.list, item];
      this.setLocalStorage();
    },
    //Удаление карточки из списка
    deleteItem(index) {
      this.list.splice(index, 1);
      this.setLocalStorage();
    },
    //Добавление в локальное хранилище
    setLocalStorage() {
      localStorage.setItem("product", JSON.stringify(this.list));
    },
    //Установка листа из локального хронилища при загрузке страницы
    setList() {
      this.list = JSON.parse(localStorage.getItem("product"))
        ? JSON.parse(localStorage.getItem("product"))
        : [];
    },
    //Сортировка страницы
    setSelect(item) {
      if (item.type === "default") {
        this.setList();
      } else if (item.type === "min") {
        this.list = this.list.sort((item1, item2) => {
          return item1["price"]?.localeCompare(item2["price"]);
        });
      } else if (item.type === "max") {
        this.list = this.list.sort((item1, item2) => {
          return item2["price"]?.localeCompare(item1["price"]);
        });
      }
    },
  },
  created() {
    this.setList();
  },
};
</script>

<style lang="scss" scoped>
@import "./style/_variable";

.main {
  padding-top: 32px;
  &__header {
    display: flex;
    justify-content: space-between;
    padding-bottom: 16px;

    @media screen and (max-width: 756px) {
      flex-direction: column;
    }
  }
  &__title {
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;
    color: $color-black;

    @media screen and (max-width: 756px) {
      padding-bottom: 16px;
    }
  }
  &__content {
    display: flex;
    justify-content: space-between;

    @media screen and (max-width: 1024px) {
      flex-direction: column;
    }
  }
}
</style>
