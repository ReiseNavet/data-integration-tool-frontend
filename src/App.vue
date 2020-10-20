<template>
  <v-app>
    <Header @switch="changeView"/>
    <v-main>
      <Form 
        v-if="showForm" 
        ref="form"
        @submit="submitData" 
        :errors="errors" 
        @clearErrors="clearErrors"
      />
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
    errors: [],
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

      const url = process.env.NODE_ENV == 'production' ? 'http://dataintegrasjon.reisenavet.no:7000/' : 'http://localhost:7000' // TODO: Update for production once HTTPS works
      try {
        const response = await fetch(url, {
          method: 'POST',
          body: formData,
        })
        
        if (response.ok) {
          const responseBody = await response.json()
          this.result = responseBody.filter(row => row.confidence > 0) // TODO: Do this in backend. Now it brings too many useless rows.
          this.changeView()
        } else {
          this.$refs.form.closeDialog()
          this.errors = [ await response.json() ]
        }
      } catch(ex) {
        this.$refs.form.closeDialog()
        this.errors = [ "Server connection failed" ]
      }
    },
    changeView () {
      this.showForm=!this.showForm
    },
    reset() {
      this.showForm = true
      this.result = []
    },
    clearErrors() {
      this.errors = []
    }
  }
};
</script>

<style lang="scss">
@media (min-width: 1904px) {
  .container {
    max-width: 1185px!important;
  }
}
</style>
