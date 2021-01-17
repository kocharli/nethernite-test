<template>
  <div class="text-end mb-1">
    <small>Total results: {{ totalPackages }}</small>
  </div>
  <div class="list-group">
    <a
      v-for="(item, index) in packages"
      :key="index"
      class="list-group-item list-group-item-action"
      @click="openModal(item.package)"
    >
      <div class="d-flex w-100 justify-content-between">
        <h6 class="mb-1">{{ item.package.name }}</h6>
        <small>v. {{ item.package.version }}</small>
      </div>
    </a>
  </div>

  <PackageDetailsModal
    :class="{ 'd-block': modalVisible }"
    :selectedPackage="selectedPackage"
    @close="modalVisible = false"
  />
</template>

<script>
import { ref } from 'vue';
import PackageDetailsModal from '@/components/PackageDetailsModal.vue';

export default {
  components: { PackageDetailsModal },
  props: {
    totalPackages: Number,
    packages: Array,
  },
  setup() {
    const modalVisible = ref(false);
    const selectedPackage = ref({});

    const openModal = (value) => {
      modalVisible.value = true;
      selectedPackage.value = value;
    };

    return {
      modalVisible,
      selectedPackage,
      openModal,
    };
  },
};
</script>

<style lang="scss" scoped>
  .list-group-item {
    cursor: pointer;
  }
</style>
