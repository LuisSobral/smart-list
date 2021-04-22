<template>
  <div class="grid grid-cols-1 sm:grid-cols-12">
    <div class="relative p-4 my-2 sm:my-0">
      <img
        :src="`/images/${isFavorite ? 'star' : 'favorite'}.png`"
        class="w-1/12 sm:w-1/4 absolute inset-0 m-auto cursor-pointer"
        @click="$emit('favorite', item)"
      />
    </div>
    <nuxt-link
      class="sm:col-start-2 sm:col-span-11"
      :to="`/contact/${item.shortName}`"
    >
      <div
        class="contact flex items-center relative bg-white rounded-lg shadow-md py-4 px-8 cursor-pointer"
      >
        <div
          class="contact-bg-image w-12 h-12 rounded-full"
          :style="{ backgroundImage: `url('${item.image}')` }"
        />
        <div class="sm:flex sm:justify-between w-full ml-6">
          <span class="font-light">{{ item.name }}</span>
          <span class="block font-light"
            >Created at {{ item.created | date }}</span
          >
        </div>
      </div>
    </nuxt-link>
  </div>
</template>

<script lang="ts">
import { Contact } from '@/types/contact'
import { Component, Vue, Prop } from 'nuxt-property-decorator'

@Component({
  filters: {
    date: (str: string) => {
      try {
        return Intl.DateTimeFormat('us-EN').format(new Date(str))
      } catch (error) {
        return 'Invalida Date'
      }
    },
  },
})
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
}
</style>
