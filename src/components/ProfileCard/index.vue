<template>
  <div class="profile-card">
    <div class="profile-card-details">
      <div>
        <img
          src="@/assets/images/doctor.svg"
          class="profile-card__image"
          :alt="`Doctor-${profile.name}`"
        />
      </div>

      <div class="profile-card-info">
        <h4 class="profile-card__name">
          <span class="label">Name: </span>
          {{ profile.name }}
        </h4>
        
        <span class="profile-card__email">
          <span class="label">Email: </span>
          {{ profile.email }}
        </span>
        
        <p class="profile-cart__Specialisation">
          <span class="label"> Specialisation: </span>{{ profile.specialisation }}
        </p>

        <div class="profile-card__reaction">
          <component
            :is="heartIcon"
            class="profile-card__heart-icon"
            @click="like"
          />

          <span class="profile-card__likes-count">{{ profile.likes }}</span>
        </div>
      </div>
    </div>
    
    <div class="profile-card__comment">
      <input
        type="text"
        class="profile-card__comment-input"
        placeholder="Write your comment..."
      />
      <button class="profile-card__comment-button">Send</button>
    </div>
  </div>
</template>

<script>
import HeartFilled from "@/components/icons/HeartFilled.vue";
import HeartOutline from "@/components/icons/HeartOutline.vue";

export default {
  name: "ProfileCard",

  components: {
    HeartFilled,
    HeartOutline,
  },

  props: {
    profile: {
      type: Object,
      required: true,
    },
  },

  computed: {
    heartIcon() {
      return this.isLiked > 0 ? "HeartFilled" : "HeartOutline";
    },
  },

  data() {
    return {
      isLiked: false,
    };
  },

  methods: {
    like() {
      this.isLiked = !this.isLiked;
      this.$emit("like", this.isLiked, this.profile.id);
    },
  },
};
</script>

<style src="./index.scss" lang="scss" scoped />
