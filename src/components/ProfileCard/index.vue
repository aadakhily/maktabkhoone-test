<template>
  <div class="profile-card">
    <img
      src="@/assets/images/doctor.svg"
      class="profile-card__image"
      :alt="`Doctor-${profile.name}`"
    />

    <div class="profile-card__info">
      <h4 class="profile-card__name">
        <span class="label">Name: </span>
        {{ profile.name }}
      </h4>
      <span class="profile-card__email">
        <span class="label">Email: </span>
        {{ profile.email }}
      </span>
      <p class="profile-cart__description">
        <span class="label"> Description: </span> {{ profile.description }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProfileCard",

  props: {
    profile: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      isFollowing: false,
    };
  },
};
</script>

<style src="./index.scss" lang="scss" scoped />
