<template>
  <div class="container">
    <Filters :filtered="filters" @active="setActive" />
    <SurveyTable :activeList="active" @filter="setFilteredData" />
  </div>
</template>

<script>
import SurveyTable from "./SurveyTable.vue";
import Filters from "./Filters.vue";

export default {
  name: "Layout",
  data() {
    return {
      filters: null,
      active: null,
    };
  },
  components: {
    SurveyTable,
    Filters,
  },
  methods: {
    setFilteredData(value) {
      this.filters = value;
    },
    setActive(value) {
      this.active = value;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
