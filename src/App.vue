<template>
  <div class="vh-100">
    <Packages />
    <Footer />
  </div>
</template>

<script>
import Packages from '@/components/Packages.vue';
import Footer from '@/components/layout/Footer.vue';

export default {
  name: 'App',
  components: {
    Packages,
    Footer,
  },
};
</script>
