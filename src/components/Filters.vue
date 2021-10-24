<template>
  <div class="filterWrapper mb-4">
    <h5 class="mb-2 filterText">Undersökningstyp</h5>
    <div class="btnWrapper mb-3">
      <button
        class="btn responsive surveytype-button"
        v-for="(surveyType, index) in activeSurveyTypes"
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
        v-bind:class="{ active: activeFavorites.all }"
        @click="setActive('all')"
      >
        Alla
      </button>
      <button
        class="btn responsive btn-secondary"
        v-bind:class="{ active: activeFavorites.favorites }"
        @click="setActive('favorites')"
      >
        Favoriter
      </button>
    </div>
  </div>
</template>

<script>
// import surveys from "../data/surveys.json";

export default {
  name: "Filters",
  data() {
    return {
      activeFavorites: { all: true, favorites: false },
      activeSurveyTypes: {
        Alla: true,
        "CSC Bostad": false,
        "CSC Lokal": false,
        Felanmälan: false,
        Inflytt: false,
        Utflytt: false,
      },
    };
  },
  methods: {
    setActive(btnName) {
      const value = this.activeFavorites[btnName];
      this.activeFavorites = { all: false, favorites: false };
      if (!value) {
        this.activeFavorites[btnName] = true;
      }
      this.$emit("active", this.activeFavorites);
    },
    setActiveSurveyType(surveyType) {
      const value = this.activeSurveyTypes[surveyType];
      for (var key in this.activeSurveyTypes) {
        this.activeSurveyTypes[key] = false;
      }
      if (!value) {
        this.activeSurveyTypes[surveyType] = true;
      }
      this.$emit(
        "surveyTypes",
        JSON.parse(JSON.stringify(this.activeSurveyTypes))
      );
    },
  },
  created() {
    // surveys.data.listSurveys.forEach((survey) => {
    //   const name = survey.survey_type;
    //   this.activeSurveyTypes[name] = false;
    // });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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