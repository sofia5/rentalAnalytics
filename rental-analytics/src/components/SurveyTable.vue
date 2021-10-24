<template>
  <div>
    <b-table
      hover
      dark
      borderless
      :items="items"
      :fields="fields"
      class="survey-table"
    >
      <template #row(0)> </template>
      <template #cell(answer_rate_latest)="data">
        {{ Math.round(data.value) + "%" }}
      </template>
      <template #cell(favorite_id)="data">
        <font-awesome-icon
          icon="heart"
          @click="setActive(data.value, data.item)"
          :class="data.value > 0 ? 'active' : ''"
        />
      </template>
    </b-table>
  </div>
</template>

<script>
import surveys from "../data/surveys.json";
let filterList = { favorites: [] };

export default {
  name: "SurveyTable",
  props: ["activeFavorites", "activeSurveyType"],
  watch: {
    activeFavorites: function () {
      this.setFilteredData();
    },
    activeSurveyType: function () {
      this.setFilteredData();
    },
  },
  data() {
    return {
      surveyTypeSelected: "",
      fields: [
        {
          key: "survey_type",
          label: "Undersökningstyp",
          sortable: true,
        },
        {
          key: "project_name",
          label: "Projektnamn",
          sortable: true,
        },
        {
          key: "project_status",
          label: "Projektstatus",
          sortable: true,
        },
        {
          key: "date_start",
          label: "Startdatum",
          sortable: true,
        },
        {
          key: "date_end",
          label: "Avslutsdatum",
          sortable: true,
        },
        {
          key: "integration",
          label: "Integration",
          sortable: true,
        },
        {
          key: "respondent_count",
          label: "Antal respondenter",
          sortable: true,
        },
        {
          key: "answer_rate_latest",
          label: "Svarsprocent",
          sortable: true,
        },
        {
          key: "favorite_id",
          label: "Favorit",
        },
      ],
      items: surveys.data.listSurveys,
    };
  },

  methods: {
    setActive(fav_id, item) {
      const index = this.items.map((i) => i === item).indexOf(true);
      if (fav_id.length === 0) {
        this.items[index].favorite_id = Math.floor(Math.random() * 100);
        filterList.favorites.push(item);
      } else {
        this.items[index].favorite_id = null;
        filterList.favorites.pop(item);
      }
    },
    setFilteredData() {
      let emptyFavorites = false;
      let emptySurveyTypes = false;

      if (this.activeFavorites) {
        if (this.activeFavorites.all) {
          emptyFavorites = true;
        }
      } else {
        emptyFavorites = true;
      }

      for (var key in this.activeSurveyType) {
        if (this.activeSurveyType[key]) {
          this.surveyTypeSelected = key;
        }
      }

      if (this.surveyTypeSelected === "Alla" || !this.surveyTypeSelected) {
        emptySurveyTypes = true;
      }

      if (emptyFavorites && emptySurveyTypes) {
        this.items = surveys.data.listSurveys;
      } else if (emptyFavorites) {
        this.items = surveys.data.listSurveys.filter(
          (i) => i.survey_type === this.surveyTypeSelected
        );
      } else if (emptySurveyTypes) {
        this.items = filterList.favorites;
      } else {
        this.items = filterList.favorites;
        this.items = this.items.filter(
          (i) => i.survey_type === this.surveyTypeSelected
        );
      }
    },
  },
};
</script>

<style scoped>
.survey-table {
  color: #ced4da;
}
.active {
  color: rgb(242, 73, 73);
}
</style>