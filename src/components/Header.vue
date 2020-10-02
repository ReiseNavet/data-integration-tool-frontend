<template>
    <v-app-bar
      app
      color="orange"
    >
      <div class="d-flex justify-center w-100">
        <v-img
          contain
          class="mr-2"
          src='../assets/logo.png'
          transition="scale-transition"
          height="60"
        />
      </div>
      <div class="col">
        <button type="button" class="btn btn-primary" @click="submit">Switch view</button>
      </div>
    </v-app-bar>
</template>

<script>
export default {
  components: {},
  props: {},
  data: () => ({
  }),
  computed: {
  },
  methods: {
    submit() {
      this.$emit('submit')
    },
  },
  mounted() {
  }
}
</script>

<style lang="scss">
  
</style>
