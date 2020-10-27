<template>
    <v-app-bar app color="orange">
      <v-row justify="center" align="center">
        <h1 
          class="text-h2 browndarken4--text user-select-none"
        >
          ReiseNavet
        </h1>

        <!-- Button to switch view. Should only be visible during development -->
        <!-- <v-btn id="switch-view-button" type="button" class="btn" @click="toggleView">Switch view</v-btn> -->
      </v-row>
    </v-app-bar>
</template>

<script>
export default {
  methods: {
    toggleView() {
      this.$emit('switch')
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
