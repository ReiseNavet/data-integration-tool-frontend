<template>
  <v-app>
    <Header @submit="changeView"/>
    <v-main>
      <Form v-if="active" @submit="changeView"/>
      <Result v-if="!active"/>
    </v-main>
  </v-app>
</template>

<script>
import Header from './components/Header'
import Form from './views/Form'
import Result from './views/Result'

export default {
  components: {
    Header,
    Form,
    Result,
  },
  data: () => ({
    active: true,
  }),
  methods: {
    changeView () {
      this.active=!this.active
    }
  }
};
</script>

<style lang="scss">

</style>