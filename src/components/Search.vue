<template>
  <input
    v-model="localValue"
    v-bind="$attrs"
    class="search w-100 d-block px-2"
    type="text"
    placeholder="Package name..."
  />
</template>

<script>
import { computed } from 'vue';

export default {
  name: 'Search',
  props: {
    modelValue: String,
  },
  emits: ['update:modelValue'],
  setup(props, context) {
    const localValue = computed({
      get: () => props.modelValue,
      set: (value) => context.emit('update:modelValue', value),
    });
    return { localValue };
  },
};
</script>

<style lang="scss" scoped>
  .search {
    height: 50px;
  }
</style>
