<template>
  <v-app light>
    <v-overlay :value="progress" color="white" opacity="1" z-index="99">
      <v-progress-circular
        color="primary"
        indeterminate
        size="64"
        width="15"
      ></v-progress-circular>
    </v-overlay>
    <v-main>
      <Nuxt />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      progress: true,
      testOngoing: false,
      dev: false,

      showPassword: false,
      passwordDev: '',
      errMsg: '',
    }
  },
  computed: {},
  created() {},
  mounted() {
    this.progress = false
  },
  methods: {},
}
</script>

<style scoped>
@import '~/assets/styles.css';
/* .v-main {
  padding-top: 90px !important;
}

.d-none {
  display: none !important;
}
@media only screen and (max-width: 600px) {
  .v-main {
    padding-top: 90px !important;
  }
} */
</style>
