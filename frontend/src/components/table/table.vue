<template>
  <div class="table">
    <div v-for="(column, index) in dataTable" :key="index">
      <table-column :column="column"></table-column>
    </div>
  </div>
</template>

<script>
import TableColumn from './column/column';

export default {
  data() {
    return {
      dataTable: [
        {
          name: 'Date',
          rows: ['11.05.2019', '15.05.2019'],
          type: 'Date',
        },
        {
          name: 'Place',
          rows: ['Гора Тахталы', 'Каньон Гейнюк'],
          type: 'String',
        },
        {
          name: 'Description',
          rows: [
            'На машине доехать до Çukuryayla  и потом 4км пешком в одну сторону',
            'Виды крутые, вода холодная, спортсменом быть желательно, но не обязательно',
          ],
          type: 'String',
        },
        {
          name: 'Lunch',
          rows: ['супермаркет (заранее)', 'кафе/супермаркет в селе Гейнюк'],
          type: 'String',
        },
        {
          name: 'Cost',
          rows: ['15', '13'],
          type: 'Finance',
        },
        {
          name: 'Transport',
          rows: [4, 1],
          type: 'Select',
        },
        {
          name: 'Rating',
          rows: ['8', '10'],
          type: 'String',
        },
      ],
    };
  },
  components: {
    TableColumn,
  },
};
</script>

<style lang="scss">
.table {
  display: flex;
  flex-direction: row;
  width: fit-content;
  height: fit-content;
  max-width: 80vw;
  max-height: 80vh;
  box-shadow: 0 0px 8px 0 white;

  div {
    height: inherit;
  }
}
</style>
