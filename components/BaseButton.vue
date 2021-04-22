<template>
  <button
    class="font-medium"
    :class="{
      'fab-btn rounded-full fixed p-5': fab,
      'rounded-xl py-2 px-5': !fab,
    }"
    @click="$emit('click')"
  >
    <span>
      <slot />
    </span>
  </button>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'nuxt-property-decorator'

@Component
export default class BaseButtonComponent extends Vue {
  @Prop({ type: Boolean, default: false }) readonly fab!: boolean
}
</script>

<style lang="scss" scoped>
button {
  outline: 0;
  color: white;
  background-color: $bg-button;

  &.fab-btn {
    right: 25px;
    bottom: 25px;
  }
}
</style>
