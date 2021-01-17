<template>
  <nav class="m-auto">
    <ul class="pagination justify-content-center mt-3">
      <li class="page-item" @click="prevPage">
        <span class="page-link" aria-label="Previous">
          <span aria-hidden="true">&laquo;</span>
        </span>
      </li>
      <template v-for="(n, index) in range" :key="index">
        <li
          v-if="n >= currentPage - 4 && n <= currentPage + 10"
          class="page-item"
          :class="{ 'active': n === currentPage }"
          @click="$emit('update:currentPage', n)"
        >
          <span class="page-link">{{ n }}</span>
        </li>
      </template>
      <li class="page-item" @click="nextPage">
        <span class="page-link" aria-label="Next">
          <span aria-hidden="true">&raquo;</span>
        </span>
      </li>
    </ul>
  </nav>
</template>

<script>
import { computed } from 'vue';

export default {
  name: 'Pagination',
  emits: ['update:currentPage'],
  props: {
    totalPages: Number,
    currentPage: Number,
  },

  setup(props, context) {
    const isFirstPage = computed(() => props.currentPage === 1);
    const isLastPage = computed(() => props.currentPage === props.totalPages);

    const range = computed(() => {
      if (props.totalPages < 0) return props.totalPages;

      return (props.currentPage + 4) > props.totalPages
        ? props.currentPage + (props.totalPages - props.currentPage)
        : props.currentPage + 4;
    });

    const prevPage = () => !isFirstPage.value && context.emit('update:currentPage', props.currentPage - 1);
    const nextPage = () => !isLastPage.value && context.emit('update:currentPage', props.currentPage + 1);

    return { nextPage, prevPage, range };
  },
};
</script>

<style lang="scss" scoped>
  .page-item {
    cursor: pointer;
  }
</style>
