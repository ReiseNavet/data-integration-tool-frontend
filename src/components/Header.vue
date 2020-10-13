<template>
    <v-app-bar app color="orange">
      <v-row justify="center" align="center">
        <h1 class="text-h2 white--text user-select-none">ReiseNavet</h1>
        <v-btn id="switch-view-button" type="button" class="btn" @click="submit">Switch view</v-btn>
      </v-row>
    </v-app-bar>
</template>

<script>
export default {
  methods: {
    submit() {
      this.$emit('submit')
    },
  },
}
</script>

<style lang="scss">
  #switch-view-button {
    position: absolute;
    right: 10px;
  }

  .user-select-none {
    user-select: none;
  }
</style>
