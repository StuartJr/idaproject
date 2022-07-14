<template>
  <div class="sorting">
    <div class="sorting__wrapper">
      <button :class="['sorting__btn', 'sorting__btn--select', {'_active': isVisible}]"
							@click="isVisible = !isVisible">
				{{ select }}
			</button>
      <div :class="['sorting__popup', {'_active' : isVisible}]">
        <ul class="sotrign__list">
          <li
            class="sorting__item"
            v-for="item in getFilterList"
            :key="item.id"
          >
            <button class="sorting__btn" @click="setSelect(item)">
              {{ item.title }}
            </button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "product-sorting",
  data() {
    return {
      list: [
        {
          id: 1,
          title: "По умолчанию",
					type: 'default',
        },
        {
          id: 2,
          title: "По цене min",
					type: 'min',
        },
        {
          id: 3,
          title: "По цене max",
					type: 'max',
        },
      ],
      select: "По умолчанию",
			isVisible: false,
    };
  },
  computed: {
    getFilterList() {
      return this.list.filter((item) => item.title !== this.select);
    },
  },
  methods: {
    setSelect(item) {
      this.select = item.title;
			this.isVisible = false;
			this.$emit('setSelectHandler', item);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./../style/_variable";
.sorting {
  position: relative;

  &__popup {
    position: absolute;
    z-index: 2;
    border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    width: 100%;
		opacity: 0;
		height: 0;
		overflow: hidden;
		transition: all .3s ease;

		&._active {
			opacity: 1;
			height: auto;
		}
  }
  &__btn {
    background: $color-light-grey;
    padding: 10px 16px 11px;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    color: $color-grey;
    width: 100%;
    display: flex;
    justify-content: flex-start;
    white-space: nowrap;
    min-width: 122px;

    &--select {
      padding: 10px 28px 11px 16px;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      &:after {
        content: "";
        display: block;
        width: 5px;
        height: 5px;
        background-color: transparent;
        position: absolute;
        right: 16px;
        top: 18px;
        transform: rotate(225deg);
        border-bottom: 1px solid $color-grey;
        border-right: 1px solid $color-grey;
				transition: all .3s ease;
      }
      &._active {
        &:after {
          transform: rotate(45deg);
					top: 14px;
        }
      }
    }
  }
}
</style>
