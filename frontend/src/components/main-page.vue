<template>
  <div class="main-page">
    <data-table/>
  </div>
</template>

<script>
import DataTable from './table/table';

export default {
  components: {
    DataTable,
  },
};
</script>

<style scoped lang="scss">
@import "../assets/styles";
.main-page {
  display: flex;
  position: absolute;
  top: 7rem;
  left: 18rem;
}
</style>
