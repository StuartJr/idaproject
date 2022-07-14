<template>
  <div class="main">
    <div class="container">
      <div class="main__header">
        <h2 class="main__title">Добавление товара</h2>
        <ProductSorting />
      </div>
      <div class="main__content">
        <ProductForm />
        <ProductList />
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
    return {};
  },
};
</script>

<style lang="scss" scoped>

$color-black: #3F3F3F;

.container {
  width: 100%;
  max-width: 1440px;
  padding: 0 32px;
}

.main {
	&__title {
		font-family: 'Source Sans Pro';
		font-style: normal;
		font-weight: 600;
		font-size: 28px;
		line-height: 35px;
		color: $color-black;
	}
}

</style>
