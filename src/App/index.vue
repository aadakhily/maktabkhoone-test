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

        <button class="new-profile-btn" @click="openCreateProfileModal">New Profile</button>
      </div>
    </header>

    <main class="app__content">
      <TransitionGroup name="list">
        <ProfileCart
          v-for="profile in searchResult"
          :profile="profile"
          :key="profile.id"
          @like="likeHandler"
          v-memo="[profile.id, profile.likes]"
        />
      </TransitionGroup>
    </main>

    <Modal :show="showModal" @close="closeCreateProfileModal">
      <CreateProfileForm @submitForm="addNewProfile" />
    </Modal>
  </div>
</template>

<script>
//fake data
import data from "../../data.json";

// components
import Modal from "@/components/Modal/index.vue";
import ProfileCart from "@/components/ProfileCard/index.vue";
import CreateProfileForm from "@/components/CreateProfileForm/index.vue";

// icon components
import TopArrow from "@/components/icons/TopArrow.vue";
import SearchIcon from "@/components/icons/SearchIcon.vue";
import BottomArrow from "@/components/icons/BottomArrow.vue";

export default {
  name: "TheApp",

  components: {
    Modal,
    TopArrow,
    SearchIcon,
    BottomArrow,
    ProfileCart,
    CreateProfileForm,
  },

  data() {
    return {
      profiles: [],
      searchInput: "",
      showModal: false,
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

    openCreateProfileModal() {
      this.showModal = true;
    },

    closeCreateProfileModal() {
      this.showModal = false;
    },

    addNewProfile(newProfile) {
      const uuid = Math.random().toString(36).substring(2, 15);

      this.profiles.push({
        ...newProfile,
        id: uuid,
        likes: 0,
      });

      this.closeCreateProfileModal();
    },

    likeHandler(isLiked, profileId) {
      const profile = this.profiles.find((profile) => profile.id === profileId);
      isLiked ? profile.likes++ : (profile.likes -= 2);
    },
  },

  computed: {
    searchResult() {
      return this.profiles.filter((item) => {
        const searchIput = this.searchInput.toLowerCase();
        const itemName = item.name.toLowerCase();

        return itemName.includes(searchIput);
      });
    },
  },
  beforeMount() {
    this.fetchData();
  },
};
</script>

<style src="./index.scss" lang="scss" />
