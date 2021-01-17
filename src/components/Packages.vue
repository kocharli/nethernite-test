<template>
  <div class="packages container py-4">
    <Search v-model="searchString" />
    <ErrorMessage v-if="hasError" />
    <div class="position-relative mt-4">
      <LoadingOverlay v-if="loading" />
      <template v-if="packages.length > 0">
        <PackagesList :totalPackages="totalPackages" :packages="packages" />
        <Pagination v-model:currentPage="currentPage" :totalPages="totalPages" />
      </template>
      <template v-else>
        <div class="text-center mt-5">
          ...no packages found
          <span>&#128528;</span>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
import { computed, onMounted, ref, watch } from 'vue';
import axios from '@/axios';
import Pagination from '@/components/Pagination.vue';
import Search from '@/components/Search.vue';
import LoadingOverlay from '@/components/LoadingOverlay.vue';
import PackagesList from '@/components/PackagesList.vue';
import ErrorMessage from '@/components/ErrorMessage.vue';

export default {
  name: 'Packages',
  components: {
    Pagination,
    Search,
    LoadingOverlay,
    PackagesList,
    ErrorMessage,
  },

  setup() {
    const searchString = ref('');
    const packages = ref([]);
    const totalPackages = ref(0);
    const currentPage = ref(1);
    const offset = ref(0);
    const loading = ref(false);
    const hasError = ref(false);

    const totalPages = computed(() => Math.ceil(totalPackages.value / 10));

    const fetchPackages = async () => {
      loading.value = true;
      hasError.value = false;

      await axios.get(`/-/v1/search?text=${searchString.value}&size=10&from=${offset.value}`)
        .then((response) => {
          packages.value = response.data.objects;
          totalPackages.value = response.data.total;
        })
        .catch(() => {
          hasError.value = true;
        }).finally(() => {
          loading.value = false;
        });
    };

    onMounted(() => fetchPackages());

    watch([currentPage, searchString], ([page]) => {
      offset.value = page !== 1 ? page * 10 : 0;
      fetchPackages();
    });

    return {
      packages,
      totalPackages,
      totalPages,
      currentPage,
      loading,
      searchString,
      hasError,
    };
  },
};
</script>

<style lang="scss" scoped>
  .packages {
    min-height: 75%;
  }
</style>
