<script lang="ts" setup>
import { defineProps } from 'vue';

// Equalent js 
// const $props = defineProps({
//   class: {
//     type: String,
//     default: 'bg-grey-100'
//   }
// })

type CardProps = {
  class?: string
}

const $props = withDefaults(defineProps<CardProps>(), {
  class: 'bg-grey-100'
})

</script>

<template>
  <div :class="$props.class" class="p-6 rounded-lg shadow-md">
    <slot />
  </div>
</template>
