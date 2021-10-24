<template>
  <div
    class="filterWrapper mb-4"
    v-if="filtered.length > 0 || filtered.favorites.length > 0"
  >
    <h5 class="mb-2 filterText">View</h5>
    <div class="btnWrapper">
      <button
        class="btn responsive btn-secondary show-button"
        v-bind:class="{ active: activeButton.all }"
        @click="setActive('all')"
      >
        All
      </button>
      <button
        class="btn responsive btn-secondary"
        v-bind:class="{ active: activeButton.favorites }"
        @click="setActive('favorites')"
      >
        Favorites
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Filters",
  props: ["filtered"],
  data() {
    return {
      activeButton: { all: true, favorites: false },
    };
  },
  methods: {
    setActive(btnName) {
      const value = this.activeButton[btnName];
      this.activeButton = { all: false, favorites: false };
      if (!value) {
        this.activeButton[btnName] = true;
      }
      this.$emit("active", this.activeButton);
    },
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