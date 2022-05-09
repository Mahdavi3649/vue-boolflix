<template>
  <div id="app">
    <header>
      <div class="d-flex">
        <img src="@/assets/img/logo2.jpg" />
      </div>

      <form class="d-flex">
        <input
          class="form-control me-2"
          type="search"
          placeholder="Search"
          aria-label="Search"
        />
        <button
          class="btn btn-outline-danger d-flex align-items-center"
          type="submit"
        >
          <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
          Search
        </button>
      </form>
    </header>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
};
</script>

<style lang="scss">
@import "@/assets/scss/style.scss";
</style>
