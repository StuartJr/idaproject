<template>
  <div class="card">
    <div class="card__wrapper">
      <img :src="item.img" alt="img" class="card__img" />
      <div class="card__content">
        <p class="card__title">{{ item.title }}</p>
        <p class="card__desc">{{ item.desc }}</p>
        <p class="card__price">{{ item.price }} руб.</p>
      </div>
			<button class="card__delete" @click="deleteItem()">
				<img src="./../assets/svg/bucket.svg" alt="" class="card__delete-svg">
			</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "product-card",
  props: {
    item: Object,
		index: Number,
  },
  data() {
    return {};
  },
	methods: {
		deleteItem() {
			this.$emit('deleteItemHandler', this.index);
		}
	},
};
</script>

<style lang="scss" scoped>
@import "./../style/_variable";
.card {
  background: $color-light-grey;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
	max-width: 332px;
	position: relative;

	&:hover {
		.card__delete {
			opacity: 1;
		}
	}

  &__img {
		display: block;
    width: 332px;
    height: 200px;
		border-radius: 4px 4px 0px 0px;
  }
  &__content {
    padding: 16px 16px 24px;
    color: $color-black;
  }
  &__title {
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
    padding-bottom: 16px;
  }
  &__desc {
		height: 80px;
		max-width: 300px;
		overflow: hidden;
		text-overflow: ellipsis;
    font-size: 16px;
    line-height: 20px;
    margin-bottom: 32px;
  }
  &__price {
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
  }
	&__delete {
		position: absolute;
		right: -8px;
		top: -8px;
		width: 32px;
		height: 32px;
		border-radius: 10px;
		background-color: $color-red;
		box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
		display: flex;
		align-items: center;
		justify-content: center;
		opacity: 0;
		transition: all .3s ease;
	}
}
</style>
