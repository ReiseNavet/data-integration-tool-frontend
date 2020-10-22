<template>
  <v-container>
    <v-row>
      <v-col>
        <h2> Alignment Tool </h2>
      </v-col>
    </v-row>
    <v-row class="my-0">
      <v-col>
        <p> 
          This alignment tool is used to compare two schemas. 
          Upload both files, choose what semantic relation wanted and compute the alignment.
        </p>
      </v-col>
    </v-row>
      <v-row 
        class="my-0" 
        justify="center" 
      >
        <h4>Upload files</h4>
      </v-row>
      <v-row class="my-0 rn-file-upload">
        <v-col offset-sm="2" sm="4" cols="12">
          <v-file-input
            truncate-length="30" 
            placeholder="Source schema"
            show-size
            v-model="sourceSchema"
          />
        </v-col>
        <v-col sm="4" cols="12">
          <v-file-input
            truncate-length="30" 
            placeholder="Target schema"
            show-size
            v-model="targetSchema"
          />
        </v-col>
      </v-row>
      <v-row 
        class="my-0" 
        justify="center"
      >
        <h4>Choose semantic relation</h4>
      </v-row>
      <v-row justify="center" class="rn-checkboxes">
        <v-col style="width: 150px!important; flex-grow: 0;">
          <v-checkbox 
            v-model="equivalence"
            label="Equivalence"
          />
          <v-checkbox 
            v-model="subsumption"
            label="Subsumption"
          />
        </v-col>
      </v-row>
      <v-row justify="center">
        <v-btn
          color="orange"
          elevation="2"
          @click.prevent="submit"
        >   
          <v-icon dark>
            mdi-check
            </v-icon>
          Compute Alignment    
        </v-btn>
        <v-dialog
          v-model="dialog"
          persistent
          max-width="300"
        >
          <v-card>
            <v-card-title>
              This can take some time...
            </v-card-title>
            <v-card-text class="mt-4">
              <v-progress-linear
                indeterminate
                color="orange"
              />
            </v-card-text>
            <v-card-actions class="d-flex justify-center pb-4">
              <v-btn color="white" @click="dialog = false"> 
                <v-icon dark> mdi-cancel </v-icon> Cancel 
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-row>
      <v-row class="mt-5">
        <v-col>
          <v-alert
            v-model="alertFillOut"
            color="black"
            text
            dense
            dismissible
            elevation="2"
            type="error"
          >   
            <span>Problems filling out form:</span>
            <ul>
              <li v-for="error in formErrors" :key="error">{{error}}</li>
            </ul>
          </v-alert>
          <v-alert
            v-model="showBackendErrors"
            color="black"
            text
            dense
            dismissible
            elevation="2"
            type="error"
          >   
            <span>Problems when computing:</span>
            <ul>
              <li v-for="error in errors" :key="error">{{error}}</li>
            </ul>
          </v-alert>
        </v-col>
      </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'Form',
  props: {
    errors: {
      type: Array,
      required: true,
    }
  },
  data: () => ({
    sourceSchema: null,
    targetSchema: null,
    equivalence: false,
    subsumption: false,
    alert: false,
    dialog: false,
    alertFillOut: false,
    formErrors: [],
  }),
  computed: {
    formData() {
      return {
        sourceSchema: this.sourceSchema,
        targetSchema: this.targetSchema,
        equivalence: this.equivalence,
        subsumption: this.subsumption,
      }
    },
    showBackendErrors: {
      get() {
        return this.errors.length > 0
      }, 
      set() {
        this.$emit('clearErrors')
      }
    }
  },
  methods: {
    validate () {
      const errs = []
      if(this.sourceSchema && this.sourceSchema.size > 2000000) {
        errs.push("Maximum filesize for sourcefile is 2 MB")
      }
      if(this.targetSchema && this.targetSchema.size > 2000000) {
        errs.push("Maximum filesize for targetfile is 2 MB")
      }
      if(!this.sourceSchema) {
        errs.push("Source file must be uploaded")
      }
      if(!this.targetSchema) {
        errs.push("Target file must be uploaded")
      }
      if(!this.equivalence && !this.subsumption) {
        errs.push("Semantic relation is required")
      } 
      this.formErrors = errs
      this.alertFillOut = this.formErrors.length > 0
      return !this.alertFillOut
    },
    submit() {
      if (this.validate()) {
        this.$emit('submit', this.formData)
        this.dialog = true
      }
    },
    closeDialog() {
      this.dialog = false
    }
  },
}
</script>

<style lang="scss">
  .rn-file-upload .v-input__slot {
    cursor: pointer!important;
  }
</style>
