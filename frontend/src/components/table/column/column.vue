<template>
  <div class="table-column" @click="click">
    <div class="header">{{column.name}}</div>
    <div class="column-body" v-for="(row, index) in column.rows" :key="index">
      <textarea-custom
        v-if="column.type==='String'"
        :value="row"
        :index="index"
        @value="saveNewValue($event, index)"
      />
      <VueCtkDateTimePicker v-else-if="column.type==='Date'" v-model="date" />
      <dropdown-menu v-else-if="column.type==='Select'" :items="transport"/>
    </div>
  </div>
</template>

<script>
import TextareaCustom from '../../textarea-custom';
import DatePicker from './date/date-picker';
import DropdownMenu from './dropdown-menu';

export default {
  props: ['column'],

  data() {
    return {
      date: '',
      transport: [
        { name: 'car', id: 1 },
        { name: 'plane', id: 2 },
        { name: 'bike', id: 3 },
        { name: 'долмуш', id: 4 },
      ],
    };
  },

  methods: {
    saveNewValue(value, index) {
      this.column.rows[index] = value;
    },
    click() {
      this.$emit('click');
    },
  },
  components: {
    TextareaCustom,
    DatePicker,
    DropdownMenu,
  },
};
</script>

<style scoped lang="scss">
.table-column {
  display: flex;
  height: fit-content;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: gray;
  opacity: 0.9;
  cursor: pointer;

  .header {
    display: flex;
    align-items: center;
    min-height: 2rem;
  }

  .column-body {
    display: flex;
    align-items: center;
  }
}
</style>
