<template>
  <form
    class="d-flex"
    @submit.prevent="$emit('searchMovie')"
    v-bind:value="searchText"
    v-on:input="$emit('input', $event.target.value)"
  >
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
      Search
    </button>
  </form>
</template>

<script>
export default {
  name: "searchBox",
  props: {
    searchText: String,
  },
};
</script>

<style lang="scss" scoped></style>
