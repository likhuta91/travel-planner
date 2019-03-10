<template>
  <div class="dropdown-menu">
    <div
      class="dropdown-list"
      :class="[(dropdownListShow && enabled) ? 'clicked' : 'default']"
      @click.stop="dropdownMenuClicked()"
    >
      <span class="dropdown-list-current-item" v-text="clickedItem.name"></span>
      <div v-if="dropdownListShow" class="dropdown-list-items">
        <div
          class="dropdown-list-item"
          v-for="item in items"
          :key="item.name"
          @click="itemClicked(item)"
        >
          <span>{{item.name}}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['items'],

  data() {
    return {
      dropdownListShow: false,
      clickedItem: '',
      enabled: true,
    };
  },

  created() {
    this.clickedItem = this.items[0];
    this.itemClicked(this.clickedItem);
  },

  methods: {
    itemClicked(item) {
      this.clickedItem = item;
      this.$emit('clickedItemName', item.name);
    },

    clicked() {
      document.removeEventListener('click', this.clicked);
      this.dropdownListShow = false;
    },

    dropdownMenuClicked() {
      if (!this.enabled) {
        return;
      }
      if (!this.dropdownListShow) {
        document.addEventListener('click', this.clicked);
      } else {
        document.removeEventListener('click', this.clicked);
      }

      this.dropdownListShow = !this.dropdownListShow;
    },
  },
};
</script>

<style scoped lang="scss">
@import "@/assets/styles.scss";

.dropdown-menu {
  display: flex;
  width: 10rem;
  height: fit-content;
  min-height: 3rem;

  .dropdown-list {
    display: flex;
    align-items: center;
    position: relative;
    width: inherit;
    height: auto;
    border-width: 1px;
    border-radius: 2px;
    background-color: $background-main;
    cursor: pointer;

    .dropdown-list-current-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      white-space: nowrap;
      width: 100%;
      margin-left: 0.5rem;
      font-size: 16px;
      line-height: 1.25;
      color: $text-color;
      text-overflow: clip;
      overflow: hidden;
      pointer-events: none;
    }

    .icon-action-visibility {
      margin: 0 0.5rem;
    }

    .dropdown-list-items {
      width: 100%;
      position: absolute;
      box-sizing: border-box;
      height: fit-content;
      overflow: hidden;
      z-index: 1;
      box-shadow: 0 0 6px 0 $box-shadow-deep;
      background-color: $background-main;
      cursor: pointer;

      .dropdown-list-item {
        display: flex;
        justify-content: flex-end;
        align-items: center;
        height: 2rem;

        span {
          width: 17rem;
          text-align: left;
          white-space: nowrap;
          font-size: 15px;
          line-height: 1.6;
          color: $text-color;
        }

        &:hover {
          background-color: $background-button;
        }
      }
    }
  }

  .default {
    border: solid 1px $gray-middle;
  }

  .clicked {
    border: solid 1px $element-checked;
  }
}
</style>
