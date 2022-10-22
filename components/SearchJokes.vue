<template>
  <form @submit.prevent="onSubmit">
    <input
      class="search-bar"
      type="text"
      v-model="text"
      placeholder="Search Jokes..."
    />
    <input class="search-btn" type="submit" value="Search Jokes" />
  </form>
</template>

<script>
export default {
  name: "SearchJokes",
  data() {
    return {
      text: "",
    };
  },
  methods: {
    onSubmit() {
      this.$emit("search-text", this.text);
      this.text = "";
    },
  },
};
</script>

<style>
.search-bar {
  padding: 7px 15px;
}
.search-btn {
  padding: 7px 11px;
  cursor: pointer;
}
</style>
