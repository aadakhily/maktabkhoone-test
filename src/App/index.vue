<template>
  <div class="app">
    <header class="app__header">
      <h1>Profiles List</h1>
    </header>

    <main class="app__content">
      <ProfileCart
        v-for="profile in profiles"
        :profile="profile"
        :key="profile.id"
      />
    </main>
  </div>
</template>

<script>
import ProfileCart from "@/components/ProfileCard/index.vue";

import data from "../../data.json";
export default {
  name: "TheApp",

  components: {
    ProfileCart,
  },

  data() {
    return {
      profiles: [],
    };
  },

  methods: {
    fetchData() {
      this.profiles = data.profiles;
    },
  },

  mounted() {
    this.fetchData();
  },
};
</script>

<style src="./index.scss" lang="scss" />
