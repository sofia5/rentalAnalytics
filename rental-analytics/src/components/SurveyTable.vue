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
  props: ["activeList"],
  watch: {
    activeList: function (activeList) {
      if (activeList.favorites) {
        this.items = filterList.favorites;
      } else {
        this.items = surveys.data.listSurveys;
      }
    },
  },
  data() {
    return {
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
          label: "Favorite",
        },
      ],
      items: surveys.data.listSurveys,
    };
  },

  methods: {
    setActive(fav_id, item) {
      const index = surveys.data.listSurveys
        .map((i) => i === item)
        .indexOf(true);

      if (fav_id.length === 0) {
        surveys.data.listSurveys[index].favorite_id = Math.floor(
          Math.random() * 100
        );
        filterList.favorites.push(item);
      } else {
        surveys.data.listSurveys[index].favorite_id = null;
        filterList.favorites.pop(item);
      }
      this.$emit("filter", filterList);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.survey-table {
  color: #ced4da;
}
.active {
  color: rgb(242, 73, 73);
}
</style>
