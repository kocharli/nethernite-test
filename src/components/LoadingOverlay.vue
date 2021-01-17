<template>
  <div
    class="spinner-overlay position-absolute w-100 h-100
    d-flex justify-content-center align-items-center"
  >
    <div class="spinner-grow text-primary" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .spinner-overlay {
    z-index: 50;
    background-color: #FFFFFF;
  }
</style>
