<template>
  <div class="app">
    <header class="app__header">
      <h1>Profiles List</h1>
      <div class="search-container">
        <div class="search">
          <div class="search__input">
            <SearchIcon />

            <input type="text" placeholder="Search..." />
          </div>

          <div class="search__sort">
            <TopArrow class="icon" />
            <BottomArrow class="icon" />
          </div>
        </div>
        <button class="new-profile-btn">New Profile</button>
      </div>
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
//fake data
import data from "../../data.json";

// components
import ProfileCart from "@/components/ProfileCard/index.vue";

// icon components
import TopArrow from "@/components/icons/TopArrow.vue";
import SearchIcon from "@/components/icons/SearchIcon.vue";
import BottomArrow from "@/components/icons/BottomArrow.vue";

export default {
  name: "TheApp",

  components: {
    TopArrow,
    SearchIcon,
    BottomArrow,
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
