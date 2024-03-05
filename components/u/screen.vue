<template>
  <USpace mode="center" block="def" full class="screen-tip">
    <USpace display="row" gap="sm" style="max-width: 12rem; text-align: left">
      <template v-if="type === 'empty'">
        <UIcon :name="ICON_EMPTY" size="md" />
        <UText :text="$t('u.emptyTip')" />
      </template>
      <template v-else-if="type === 'loading'">
        <UIcon :name="ICON_LOADING_CIRCLE" size="md" />
      </template>
      <template v-else-if="type === 'error'">
        <UIcon name="tabler:table-down" size="md" />
        <UText :text="$t('u.errorTip')" />
      </template>
    </USpace>
  </USpace>
</template>

<script setup lang="ts">
withDefaults(defineProps<{ type?: 'loading' | 'empty' | 'error' }>(), { type: 'loading' })
</script>

<style scoped lang="scss">
.screen-tip {
  height: 100%;
  border-radius: 0;
  border-right: 0;
  border-left: 0;
}
</style>
