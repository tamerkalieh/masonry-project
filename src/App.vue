<template>
  <div>
    <div class='masonry'>
      <div class='masonry__gallery'>
        <div
          v-for="(image, index) in images"
          :key="index"
          class='masonry__item'
        >
          <Transition>
            <FlagSelect
              v-if="image.showSelect"
              class='masonry__select'
              :image-index="index"
              @update-state="updateImageFlagState"
            />
          </Transition>
          <div
            :class="[
              'masonry__item-btn',
              'none' === image.state
                ? 'masonry__item-btn--hidden'
                : `masonry__item-btn--${image.state}`,
            ]"
            @click="openSelection(index)"
          >
            <svg
              class='masonry__flag-img'
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
            <span class='ml-1' v-if="'none' !== image.state">{{
              availableFlags[image.state].text
            }}</span>
          </div>
          <img class='masonry__image' :src="image.src" />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang='ts'>
import { defineComponent, ref } from 'vue'
import FlagSelect from './components/FlagSelect.vue';
import availableFlags from './resources/flags.js';
import imageResource from './resources/images.js';
import type Image from './types/Image'
import type FlagState from './types/FlagState'

export default defineComponent({
  name: 'App',
  components: { FlagSelect },
  setup() {
    const images = ref<Image[]>(imageResource)

    const updateImageFlagState = ({ index, state }) => {
      images.value[index].showSelect = false;
      images.value[index].state = state;
    }

    const openSelection = (imageIndex: Number) => {
      images.value.forEach((image) => (image.showSelect = false));
      images.value[imageIndex].showSelect = true;
    }

    return { images, availableFlags, updateImageFlagState, openSelection }
  }
});
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
      @apply absolute right-0 top-0 z-10 mr-2 md:mr-4 mt-2 md:mt-4 bg-white rounded-lg w-auto px-2 h-8 flex items-center shadow-lg text-white text-xs
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
