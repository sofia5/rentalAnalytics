<template>
  <div class="filterWrapper mb-4">
    <h5 class="mb-2 filterText">Undersökningstyp</h5>
    <div class="btnWrapper mb-3">
      <button
        class="btn responsive surveytype-button"
        v-for="(surveyType, index) in activeFilters.surveyTypes"
        :key="index"
        v-bind:class="{ active: surveyType }"
        @click="setActiveSurveyType(index)"
      >
        {{ index }}
      </button>
    </div>
    <h5 class="mb-2 filterText">Favoriter</h5>
    <div class="btnWrapper">
      <button
        class="btn responsive btn-secondary show-button"
        v-for="(favorite, index) in activeFilters.favorites"
        :key="index"
        v-bind:class="{ active: favorite }"
        @click="setActiveFavorites(index)"
      >
        {{ index }}
      </button>
    </div>
  </div>
</template>

<script>
import surveys from "../data/surveys.json";

export default {
  name: "Filters",
  data() {
    return {
      activeFilters: { favorites: {}, surveyTypes: {} },
    };
  },
  methods: {
    setActiveFavorites(name) {
      const value = this.activeFilters.favorites[name];
      this.activeFilters.favorites = { Alla: false, Favoriter: false };
      if (!value) {
        this.activeFilters.favorites[name] = true;
      }
      this.sendData();
    },
    setActiveSurveyType(surveyType) {
      const value = this.activeFilters.surveyTypes[surveyType];
      for (var key in this.activeFilters.surveyTypes) {
        this.activeFilters.surveyTypes[key] = false;
      }
      if (!value) {
        this.activeFilters.surveyTypes[surveyType] = true;
      }
      this.sendData();
    },
    sendData() {
      this.activeFilters = JSON.parse(JSON.stringify(this.activeFilters));
      this.$emit("active", this.activeFilters);
    },
  },
  created() {
    this.activeFilters.surveyTypes["Alla"] = true;
    surveys.data.listSurveys.forEach((survey) => {
      const name = survey.survey_type;
      this.activeFilters.surveyTypes[name] = false;
    });
    this.activeFilters.favorites = { Alla: true, Favoriter: false };
  },
};
</script>

<style scoped>
.filterWrapper {
  text-align: left;
}
.filterText {
  flex-basis: 100%;
  color: #30bced;
}
.surveytype-button,
.show-button {
  margin-right: 1rem;
}
.btn {
  padding-top: 0;
  padding-bottom: 0;
  font-size: smaller;
  color: #16191c;
  font-weight: 520;
  background-color: #ced4da;
}
.btn:focus {
  outline: none !important;
  box-shadow: none !important;
  border: 1px solid black;
}
.active {
  background-color: #30bced !important;
  color: #16191c !important;
}
</style>