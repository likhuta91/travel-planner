<template>
  <div class="textarea">
    <textarea
      class="visible"
      :maxlength="maxlengthSymbols"
      :placeholder="placeholder"
      :value="value"
      spellcheck="false"
      @input="onChangeData('name', $event)"
    ></textarea>
  </div>
</template>

<script>
export default {
  props: ['name', 'value', 'placeholder', 'maxlengthSymbols', 'index'],

  data() {
    return {
      hiddenDataInput: 'sss',
    };
  },
  created() {
    this.hiddenDataInput = this.value;
  },

  mounted() {
    this.updateRowHeight();
  },

  methods: {
    onChangeData(field, data) {
      const newData = data.target.value.trim();
      this.hiddenDataInput = data.target.value;
      this.$emit('value', newData);
      this.updateRowHeight();
    },

    updateRowHeight() {
      const table = document.getElementsByClassName('table')[0];
      let maxheight = 0;
      for (let i = 0; i < table.children.length; i += 1) {
        const rowElement =
          table.children[i].children[0].children[this.index + 1];
        if (rowElement.firstChild.className === 'textarea') {
          const height = rowElement.firstChild.firstChild.scrollHeight;
          if (maxheight < height) maxheight = height;
        }
      }
      const currentScrollHeight = this.$el.firstChild.scrollHeight;
      if (currentScrollHeight > maxheight) maxheight = currentScrollHeight;
      for (let i = 0; i < table.children.length; i += 1) {
        const row = table.children[i].children[0].children[this.index + 1];
        row.style.height = `${maxheight - 3}px`;
      }
    },
  },
};
</script>

<style scoped lang="scss">
@import "@/assets/styles.scss";

.textarea {
  ::placeholder {
    font-family: SegoeUI, Helvetica, Tahoma, Geneva, Verdana, Roboto, sans-serif;
    font-size: 16px;
    font-weight: normal;
    font-style: normal;
    font-stretch: normal;
    line-height: 1.25;
    letter-spacing: normal;
    color: $gray-middle;
  }

  textarea {
    padding: 0.5rem;
    min-height: 3rem;
    border-radius: 2px;
    border: solid 1px $gray-middle;
    font-size: 16px;
    line-height: 1.25;
    resize: none;
    color: $text-color;
    overflow: hidden;
    box-sizing: border-box;
    background-color: $background-main;
  }

  textarea:hover {
    border-radius: 2px;
    border: solid 1px $border-hover;
  }

  textarea:focus {
    outline: none !important;
    border-radius: 2px;
    border: 1px solid $element-checked;
  }

  .visible {
    height: inherit;
  }
  .hidden {
    position: absolute;
    visibility: hidden;
  }
}
</style>
