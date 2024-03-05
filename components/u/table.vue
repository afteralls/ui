<template>
  <ClientOnly>
    <USpace display="col" gap="none" full class="table">
      <USpace display="row" pos="between" class="info">
        <USpace display="row" gap="sm" class="table-head">
          <UIcon name="mynaui:table" size="md" class="hide" />
          <USpace display="col" gap="bit">
            <UText :text="title" style="font-weight: bold" />
            <UText gray :text="$t('u.tableName')" />
          </USpace>
        </USpace>
        <USpace display="row" class="options" :style="`display: ${print ? 'none' : 'flex'}`">
          <slot name="options" />
        </USpace>
      </USpace>
      <USpace full>
        <div v-if="loading" class="table-screen"><UScreen type="loading" /></div>
        <div v-else-if="error" class="table-screen"><UScreen type="error" /></div>
        <div v-else-if="lenght === 0" class="table-screen"><UScreen type="empty" /></div>
        <div v-else class="table-container">
          <UScroll dir="right" :class="{ 'table-scroll': true, max: print }">
            <table>
              <slot name="table" />
            </table>
          </UScroll>
        </div>
        <USpace v-if="lenght" display="row" full class="stats">
          <UText gray :text="`Количество записей: ${lenght}`" />
        </USpace>
      </USpace>
    </USpace>
    <template #fallback><UFallback type="table" /></template>
  </ClientOnly>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    title: string
    error?: any | null
    lenght?: number
    loading?: boolean
    print?: boolean
  }>(),
  {
    lenght: undefined,
    error: null
  }
)

defineEmits<{ (e: 'reload'): void }>()
defineSlots<{ options(): any; table(): any }>()
</script>

<style scoped lang="scss">
.table {
  border: toRem(1) solid var(--br);
  border-radius: var(--br-rad);
  overflow: hidden;
}

.info,
.stats {
  padding: var(--space);
}

.stats {
  border-top: toRem(1) solid var(--br);
}

.table-container {
  width: 100%;
  max-width: 100%;
  position: relative;
  overflow: hidden;
}

.table-head {
  span,
  div {
    pointer-events: none;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }

  @media (max-width: $mob) {
    max-width: toRem(250);
  }

  @media (max-width: $zf) {
    max-width: toRem(150);
  }
}

.table-scroll {
  overflow-y: scroll;
  height: fit-content;
  max-height: 50vh;
  position: inherit;
  z-index: 5;
  overflow: hidden;
}

.table-screen {
  padding-bottom: var(--space);
}

.max {
  max-height: 100% !important;
  padding-bottom: 0;
}

.hide {
  @media (max-width: $zf) {
    display: none;
  }
}
</style>
