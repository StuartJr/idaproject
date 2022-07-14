<template>
  <div class="list">
			<transition-group name="animation" tag='div' class="list__wrapper" appear>
				<ProductCard
						v-for="(item, index) in list"
						:key="item.id"
						:item="item"
						:index="index"
						@deleteItemHandler="deleteItemHandler"
					/>
			</transition-group>
  </div>
</template>

<script>
import ProductCard from "@/components/ProductCard.vue";

export default {
  name: "product-list",
  components: {
    ProductCard,
  },
  props: {
    list: Array,
  },
  data() {
    return {};
  },
	methods: {
		deleteItemHandler(index) {
			this.$emit('deleteItemHandler', index);
		}
	},
};
</script>

<style lang="scss" scoped>
.list {
	width: 100%;
  &__wrapper {
		width: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;
    max-width: 1028px;

		@media screen and (max-width: 1400px) {
			grid-template-columns: 1fr 1fr;
		}

		@media screen and (max-width: 756px) {
			grid-template-columns: 1fr;
		}
  }
}

.animation-enter-active,
.animation-leave-active {
  transition: all 0.8s;
}
.animation-enter,
.animation-leave-to {
  opacity: 0;
  transform: translateY(20%);
}
.animation-move {
  transition: all 0.5s;
}
</style>
