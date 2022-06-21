<template>
  <div class="app">
    <header class="app__header">
      <h1>Profiles List</h1>

      <div class="search-container">
        <div class="search">
          <div class="search__input">
            <SearchIcon />

            <input type="text" placeholder="Search..." v-model="searchInput" />
          </div>

          <div class="search__sort">
            <TopArrow class="icon" @click="sortAsc" />
            <BottomArrow class="icon" @click="sortDesc" />
          </div>
        </div>

        <button class="new-profile-btn">New Profile</button>
      </div>
    </header>

    <main class="app__content">
      <TransitionGroup name="list">
        <ProfileCart
          v-for="profile in searchResult"
          :profile="profile"
          :key="profile.id"
        />
      </TransitionGroup>
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
      searchInput: "",
    };
  },

  methods: {
    fetchData() {
      this.profiles = data.profiles;
    },

    sortAsc() {
      this.profiles.sort((a, b) => a.likes - b.likes);
    },

    sortDesc() {
      this.profiles.sort((a, b) => b.likes - a.likes);
    },
  },

  computed: {
    searchResult() {
      return this.profiles.filter((item) =>
        item.name.includes(this.searchInput)
      );
    },
  },

  beforeMount() {
    this.fetchData();
  },
};
</script>

<style src="./index.scss" lang="scss" />
