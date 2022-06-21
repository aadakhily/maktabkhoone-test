<template>
  <Teleport to="body">
    <transition name="fade" appear>
      <div v-if="show" class="modal-bg" @click.self="closeModal">
        <div class="modal">
          <div v-if="showHeader" class="modal__header">
            <button class="modal__back-btn" @click="closeModal">
              <CloseIcon class="icon" />
              <slot name="header">Close</slot>
            </button>
          </div>

          <div class="modal__content">
            <slot>this is modal__content</slot>
          </div>
        </div>
      </div>
    </transition>
  </Teleport>
</template>

<script>
import CloseIcon from "@/components/icons/CloseIcon.vue";

export default {
  name: "KModal",

  emits: ["close"],

  components: {
    CloseIcon,
  },

  props: {
    show: {
      type: Boolean,
      default: true,
    },

    showHeader: {
      type: Boolean,
      default: true,
    },
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
  },
};
</script>

<style src="./index.scss" lang="scss" scoped />
