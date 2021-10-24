<template>
  <div class="container">
    <Filters
      :filtered="filters"
      @active="setActive"
      @surveyTypes="setActiveSurveyTypes"
    />
    <SurveyTable
      :activeFavorites="active"
      :activeSurveyType="surveyTypes"
      @filter="setFilteredData"
    />
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
      surveyTypes: null,
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
    setActiveSurveyTypes(value) {
      this.surveyTypes = value;
    },
  },
};
</script>

