<template>
  <div v-if="isOpen" class="fixed bottom-0 left-0 lg:flex items-center p-4 bg-gray-100 shadow-sm justify-center w-full">
    <div class="text-5xl pb-2 leading-none">
        🍪
    </div>
    <div class="lg:mx-8">
        <p>
          We use cookies for analytics.
        </p>
    </div>
    <div class="flex justify-center mt-4 lg:mt-0">
        <button class="button ml-2 md:ml-0 cursor-pointer" @click="accept">Ok Great</button>
        <button class="button md:ml-2 cursor-pointer" @click="deny">Nope</button>
    </div>
  </div>
</template>

<script>
import { bootstrap } from 'vue-gtag';

export default {
  data() {
    return {
      isOpen: false
    };
  },
  created() {
    if (!this.getGDPR() === true) {
      this.isOpen = true;
    }
  },
  methods: {
    accept() {
      if (process.browser) {
        bootstrap().then(gtag => {
          this.isOpen = false;
          localStorage.setItem('GDPR:accepted', true);
          location.reload();
        })
      }
    },
    deny() {
      if (process.browser) {
        this.isOpen = false;
        localStorage.setItem('GDPR:accepted', false);
      }
    },
    getGDPR() {
      if (process.browser) {
        return localStorage.getItem('GDPR:accepted', true);
      }
    },
  }
}
</script>
