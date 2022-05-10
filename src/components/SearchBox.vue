<template>
  <form class="d-flex" @submit.prevent="$emit('formSubmit')">
    <input
      class="form-control me-2"
      type="search"
      placeholder="Search"
      aria-label="Search"
      v-bind:value="searchText"
      v-on:input="$emit('input', $event.target.value)"
      @keyup="$emit('formSubmit')"
    />
    <button
      class="btn btn-outline-danger d-flex align-items-center"
      type="submit"
    >
      <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
      Search
    </button>
  </form>
</template>

<script>
export default {
  name: "SearchBox",

  props: {
    searchText: String,
  },
};
</script>

<style lang="scss" scoped></style>
