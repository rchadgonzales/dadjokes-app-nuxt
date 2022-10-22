<template>
  <!-- <div>Jokes index</div> -->
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke
      v-for="joke in jokes"
      v-bind:key="joke.id"
      :id="joke.id"
      :joke="joke.joke"
    />
  </div>
</template>

<script>
import axios from "axios";
import Joke from "../../components/Joke.vue";
import SearchJokes from "../../components/SearchJokes.vue";

export default {
  components: {
    Joke,
    SearchJokes,
  },
  data() {
    return {
      jokes: [],
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json",
      },
    };
    try {
      const res = await axios.get("https://icanhazdadjoke.com/search", config);

      // console.log(res.data);
      this.jokes = res.data.results;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
          Accept: "application/json",
        },
      };
      try {
        const res = await axios.get(
          `https://icanhazdadjoke.com/search?term=${text}`,
          config
        );

        this.jokes = res.data.results;
      } catch (error) {
        console.log(error);
      }
    },
  },
  head() {
    return {
      title: "DadJokes",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Application for dad jokes",
        },
      ],
    };
  },
};
</script>

<style></style>
