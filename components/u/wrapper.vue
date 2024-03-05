<template>
  <USpace
    class="card"
    full
    :style="`background-color: var(--${block === 'def' ? 'fg-m' : 'auto'})`"
  >
    <USpace display="row" pos="between" style="padding: var(--space)" full>
      <USpace display="row" class="title">
        <UIcon v-if="icon" :name="icon" />
        <UText type="span" :text="title" />
      </USpace>
      <slot name="option" />
    </USpace>
    <ULine :mode="mode" />
    <USpace display="col" :style="padding ? `padding: var(--space)` : null">
      <slot />
    </USpace>
    <USpace v-if="slots.action" class="action" display="col"><slot name="action" /></USpace>
  </USpace>
</template>

<script setup lang="ts">
const slots = defineSlots<{ option?: any; default: any; action?: any }>()
withDefaults(
  defineProps<{
    title: string
    block?: 'def' | 'alt'
    icon?: string
    mode?: 'dashed'
    padding?: boolean
  }>(),
  {
    block: 'alt',
    icon: undefined,
    mode: undefined,
    padding: true
  }
)
</script>

<style scoped lang="scss">
.card {
  border: toRem(1) solid var(--br);
  border-radius: var(--br-rad);
}

.title {
  span {
    @media (max-width: $mob) {
      font-size: 0.875rem;
    }
  }
}

.action {
  padding: var(--space);
  border-top: toRem(1) solid var(--br);
}
</style>
