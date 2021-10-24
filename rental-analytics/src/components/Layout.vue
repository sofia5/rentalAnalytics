<template>
  <div class="container">
    <Filters @active="setActive" @surveyTypes="setActiveSurveyTypes" />
    <SurveyTable :activeFavorites="active" :activeSurveyType="surveyTypes" />
  </div>
</template>

<script>
import SurveyTable from "./SurveyTable.vue";
import Filters from "./Filters.vue";

export default {
  name: "Layout",
  data() {
    return {
      active: null,
      surveyTypes: null,
    };
  },
  components: {
    SurveyTable,
    Filters,
  },
  methods: {
    setActive(value) {
      this.active = value;
    },
    setActiveSurveyTypes(value) {
      this.surveyTypes = value;
    },
  },
};
</script>

