<template>
  <div class="modal">
    <div class="modal-dialog modal-lg shadow-lg">
      <div class="modal-content">
        <div class="modal-header">
          <h3 class="modal-title">
            {{ selectedPackage.name }}
            <span class="badge bg-primary">{{ selectedPackage.version }}</span>
          </h3>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
            @click="$emit('close')"
          />
        </div>
        <div class="modal-body overflow-auto">
          <div v-if="selectedPackage.author && selectedPackage.author.name" class="package-info">
            <span class="label">Author:</span>
            {{ selectedPackage.author.name }}
          </div>
          <div v-if="selectedPackage.author && selectedPackage.author.url" class="package-info">
            <span class="label">Author URL:</span>
            {{ selectedPackage.author.url }}
          </div>
          <div v-if="selectedPackage.links && selectedPackage.links.homepage" class="package-info">
            <span class="label">Homepage:</span>
            <a class="ms-1" :href="selectedPackage.links.homepage">
              {{ selectedPackage.links.homepage }}
            </a>
          </div>
          <div
            v-if="selectedPackage.links && selectedPackage.links.repository"
            class="package-info"
          >
            <span class="label">Repository:</span>
            <a class="ms-1" :href="selectedPackage.links.repository">
              {{ selectedPackage.links.repository }}
            </a>
          </div>
          <div v-if="selectedPackage.description" class="package-info">
            <div class="label">Description:</div>
            {{ selectedPackage.description }}
          </div>
          <div
            v-if="selectedPackage.keywords && selectedPackage.keywords.length > 0"
            class="package-info"
          >
            <div class="label mb-2">Keywords</div>
            <span
              v-for="(keyword, index) in selectedPackage.keywords"
              :key="index"
              class="badge bg-light text-dark me-1 mt-1 d-inline-block">
              {{ keyword }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PackageDetailsModal',
  props: {
    selectedPackage: Object,
  },
};
</script>

<style lang="scss" scoped>
  .package-info {
    margin: 0 0 10px 0;
    .label {
      font-weight: 700;
    }
  }

  .modal-content {
    max-height: 80vh;
  }
</style>
