<template>
  <div>
    <p v-if="items.length === 0" class="mt-4 font-light text-center">
      {{ emptyText }}
    </p>
    <transition-group v-else tag="div" name="fade" class="flex flex-wrap">
      <div
        v-for="item in items"
        :key="item.shortName"
        class="card-container p-2"
        :class="{ 'w-1/2 sm:w-1/3 md:w-1/4 lg:w-1/6': isVertical, 'w-full': isHorizontal }"
      >
        <vertical-card
          v-if="isVertical"
          :item="item"
          :is-favorite="isFavorite"
          @favorite="$emit('favorite', item)"
        />
        <horizontal-card
          v-else-if="isHorizontal"
          :item="item"
          :is-favorite="isFavorite"
          @favorite="$emit('favorite', item)"
        />
      </div>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { Contact } from '@/types/contact'
import { Component, Vue, Prop } from 'nuxt-property-decorator'

@Component
export default class ListCardsComponent extends Vue {
  @Prop({ type: String, default: '' }) readonly emptyText!: String
  @Prop({ type: Array, required: true }) readonly items!: Contact[]
  @Prop({ type: Boolean, default: false }) readonly isFavorite!: boolean
  @Prop({
    type: String,
    default: 'vertical',
    validator: (type) => ['vertical', 'horizontal'].includes(type),
  })
  readonly type!: string

  get isVertical(): boolean {
    return this.type === 'vertical'
  }

  get isHorizontal(): boolean {
    return this.type === 'horizontal'
  }
}
</script>

<style lang="scss" scoped>
.card-container {
  &.fade-leave-active {
    position: absolute;
  }

  &.fade-enter,
  &.fade-leave-to {
    opacity: 0;
  }

  &.fade-move {
    transition: transform 1s;
  }
}
</style>
