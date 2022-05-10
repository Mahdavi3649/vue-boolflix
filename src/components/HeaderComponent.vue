<template>
  <header>
    <div class="d-flex">
      <img src="@/assets/img/logo2.jpg" />
    </div>

    <SearchBox v-model="searchText" @formSubmit="search"></SearchBox>
  </header>
</template>

<script>
import SearchBox from "@/components/SearchBox.vue";
import state from "@/state.js";
export default {
  name: "HeaderComponent",

  components: {
    SearchBox,
  },

  data() {
    return {
      searchText: "",
    };
  },

  methods: {
    search() {
      console.log("searching ...");
      console.log(this.searchText);
      state.searchText = this.searchText;
    },
  },
};
</script>

<style scoped lang="scss">
header {
  display: flex;
  justify-content: space-between;
  background-color: black;
  padding: 15px;

  img {
    width: 130px;
  }
}
</style>
