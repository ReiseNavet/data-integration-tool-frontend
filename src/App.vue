<template>
  <v-app>
    <Header @submit="changeView"/>
    <v-main>
      <Form v-if="showForm" @submit="submitData"/>
      <Result v-else/>
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
    showForm: true,
    result: null,
  }),
  methods: {
    async submitData(data) {
      const formData = new FormData()
      formData.append('source', data.sourceSchema)
      formData.append('target', data.targetSchema)

      /**The way form-data works, is that booleans are only
       * cared about if they are true, otherwise we don't
       * put them into the package. */
      if(data.equivalence) {
        formData.append('equivalence', 'true')
      }
      if(data.subsumption) {
        formData.append('subsumption', 'true')
      }

      const url = 'http://localhost:7000' // TODO: Change for productionn

      const response = await fetch(url, {
        method: 'POST',
        body: formData,
      })
      const responseBody = await response.json()

      console.log(responseBody)

      this.result = responseBody
      
      this.changeView()

      const message = this.result.length ? `${this.result.length} rows received from backend! That's a lot! (Right..?)` : 'No rows received from backend..?'
      alert(message)
    },
    changeView () {
      this.showForm=!this.showForm
    }
  }
};
</script>

<style lang="scss">

</style>