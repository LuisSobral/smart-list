<template>
  <nuxt-link :to="`/contact/${item.shortName}`">
    <div
      class="contact relative bg-white rounded-lg shadow-md py-10 px-2 cursor-pointer"
    >
      <img
        :src="require(`@/static/images/${isFavorite ? 'star' : 'favorite'}.png`)"
        class="absolute top-3 left-4 cursor-pointer"
        @click="
          $event.stopPropagation()
          $event.preventDefault()
          $emit('favorite', item)
        "
      />
      <div
        class="contact-bg-image w-24 h-24 rounded-full mx-auto"
        :style="{ backgroundImage: `url('${item.image}')` }"
      />
      <p class="text-center mt-6 font-light">{{ item.name }}</p>
      <p
        class="contact-description h-12 overflow-ellipsis overflow-hidden text-center mt-6 font-light"
      >
        {{ item.description }}
      </p>
    </div>
  </nuxt-link>
</template>

<script lang="ts">
import { Contact } from '@/types/contact'
import { Component, Vue, Prop } from 'nuxt-property-decorator'

@Component
export default class VerticalCardComponent extends Vue {
  @Prop({ type: Object, required: true }) readonly item!: Contact
  @Prop({ type: Boolean, default: false }) readonly isFavorite!: boolean
}
</script>

<style lang="scss" scoped>
.contact {
  transition: all 1s;
  -webkit-transition: all 1s;

  &-bg-image {
    background-size: cover;
  }

  &-description {
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }
}
</style>
