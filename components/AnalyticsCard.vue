<template>
  <div class="flex items-center bg-white rounded-xl shadow-lg p-10 h-64">
    <div
      class="relative rounded-full w-20 h-20"
      :style="{ backgroundColor: bgColor }"
    >
      <img class="absolute inset-0 m-auto w-1/2" :src="iconSrc" />
    </div>
    <div class="ml-5">
      <span class="text-3xl font-bold">{{ analyticData | number }}</span>
      <span class="title text-base block font-medium">{{ title }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'nuxt-property-decorator'

@Component({
  filters: {
    number: (value: number) => {
      try {
        return Intl.NumberFormat('pt-BR').format(value)
      } catch (error) {
        return 'Invalida Value'
      }
    },
  },
})
export default class VerticalCardComponent extends Vue {
  @Prop({ type: String, required: true }) readonly title!: string
  @Prop({ type: String, required: true }) readonly iconSrc!: string
  @Prop({ type: String, required: true }) readonly bgColor!: string
  @Prop({ type: Number, required: true }) readonly analyticData!: number
}
</script>

<style lang="scss" scoped>
span {
  &.title {
    color: #939da5;
  }

  color: #617078;
}
</style>
