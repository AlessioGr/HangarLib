<script lang="ts" setup>
import Popper from "vue3-popper";

const props = withDefaults(
  defineProps<{
    hover?: boolean;
    show?: boolean | null;
  }>(),
  {
    hover: true,
    show: null,
  }
);
</script>

<template>
  <Popper :hover="hover" open-delay="200" close-delay="100" :show="show">
    <slot />
    <template #content>
      <slot name="content" />
    </template>
  </Popper>
</template>

<style>
.popper {
  --popper-theme-background-color: #464646;
  --popper-theme-padding: 0.5rem;
  --popper-theme-border-radius: 0.375rem;
  --popper-theme-text-color: #fff;
}
</style>
