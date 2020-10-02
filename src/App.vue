<template>
  <v-app>
    <Header @submit="changeView"/>
    <v-main>
      <Form v-if="showForm" @submit="submitData"/>
      <Result v-else :result="result" @reset="reset"/>
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
    result: [],
  }),
  methods: {
    async submitData(data) {
      const formData = new FormData()
      formData.append('source', data.sourceSchema)
      formData.append('target', data.targetSchema)
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
      this.result = responseBody.filter(row => row.confidence > 0) // TODO: Do this in backend. Now it brings too many useless rows.
      
      this.changeView()
    },
    changeView () {
      this.showForm=!this.showForm
    },
    reset() {
      this.showForm = true
      this.result = []
    }
  }
};
</script>

<style lang="scss">
</style>
