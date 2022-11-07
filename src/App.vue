<template>
  <div>
    <div class="masonry">
      <div class="masonry__gallery">
        <div
          v-for="(image, imgIndex) in images"
          :key="imgIndex"
          class="masonry__item"
        >
          <Transition>
            <FlagSelect
              v-if="image.showSelect"
              class="masonry__select"
              :image-index="imgIndex"
              @update-state="updateState"
            />
          </Transition>
          <div
            :class="[
              'masonry__item-btn',
              'none' === image.state
                ? 'masonry__item-btn--hidden'
                : `masonry__item-btn--${image.state}`,
            ]"
            @click="openSelection(imgIndex)"
          >
            <svg
              class="masonry__flag-img"
              enable-background="new 0 0 60 60"
              version="1.1"
              viewBox="0 0 60 60"
              xml:space="preserve"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M51.371,3.146c-0.203-0.081-5.06-1.997-10.815-1.997c-3.434,0-6.47,0.687-9.024,2.042C29.269,4.392,26.199,5,22.407,5  C17.099,5,11.865,3.788,10,3.307V1c0-0.553-0.447-1-1-1S8,0.447,8,1v3c0,0.014,0.007,0.026,0.008,0.04C8.008,4.052,8,4.062,8,4.074  V33v1.074V59c0,0.553,0.447,1,1,1s1-0.447,1-1V35.373C12.273,35.937,17.243,37,22.407,37c4.122,0,7.507-0.688,10.062-2.042  c2.263-1.201,4.983-1.81,8.087-1.81c5.357,0,10.027,1.836,10.073,1.854c0.309,0.124,0.657,0.086,0.932-0.102  C51.835,34.716,52,34.406,52,34.074v-30C52,3.665,51.751,3.298,51.371,3.146z"
              />
            </svg>
            <span class="ml-1" v-if="'none' !== image.state">{{
              flags[image.state].text
            }}</span>
          </div>
          <img class="masonry__image" :src="image.src" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import flags from "./resources/flags.js";
import FlagSelect from "./components/FlagSelect.vue";

export default {
  components: { FlagSelect },
  data() {
    return {
      flags,
      images: [
        {
          src: "https://source.unsplash.com/random/1",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/2",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/3",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/4",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/5",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/6",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/7",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/8",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/9",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/10",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/11",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/12",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/13",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/14",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/15",
          state: "none",
          showSelect: false,
        },
        {
          src: "https://source.unsplash.com/random/16",
          state: "none",
          showSelect: false,
        },
      ],
    };
  },
  methods: {
    updateState(flagUpdate) {
      this.images[flagUpdate.index].showSelect = false;
      this.images[flagUpdate.index].state = flagUpdate.state;
    },
    openSelection(imageIndex) {
      this.images.forEach((image) => (image.showSelect = false));
      this.images[imageIndex].showSelect = true;
    },
  },
};
</script>

<style scoped lang="sass">
.masonry
  @apply grid md:py-48
  &__gallery
    @apply justify-self-center self-center m-2 md:w-2/3 bg-white p-8 columns-2 md:columns-4 rounded-lg
  &__item
    $img: &
    @apply mb-4 relative
    & > #{$img}-btn
      @apply absolute right-0 top-0 z-10 mr-4 mt-4 bg-white rounded-lg w-auto px-2 h-8 flex items-center shadow-lg text-white text-xs
      &--hidden
        @apply opacity-0 transition-opacity
        & > .masonry__flag-img
          @apply fill-slate-400
      &--none
        @apply bg-white
      &--no
        @apply bg-red-400
      &--maybe
        @apply bg-orange-400
      &--yes
        @apply bg-green-400
      &--finalized
        @apply bg-black
    &:hover > .masonry__item-btn--hidden
      @apply opacity-100
  &__flag-img
    @apply h-5 w-5 rounded-lg flex justify-center items-center fill-white
  &__image
    @apply rounded-lg
  &__select
    @apply absolute z-20 -right-6 bg-white w-36 text-center px-4 py-2 shadow-xl rounded-lg transition-opacity
</style>
