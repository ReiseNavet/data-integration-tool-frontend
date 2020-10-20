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
    <v-form 
      ref="form"
      v-model="valid"
      lazy-validation
    >
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
            :rules="uploadFileRules"
            v-model="sourceSchema"
            required
          />
        </v-col>
        <v-col sm="4" cols="12">
          <v-file-input
            truncate-length="30" 
            placeholder="Target schema"
            show-size
            :rules="uploadFileRules"
            v-model="targetSchema"
            required
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
            :rules="checkboxRules"
            required
          />
          <v-checkbox 
            v-model="subsumption"
            label="Subsumption"
            :rules="checkboxRules"
            required
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
    </v-form>
  </v-container>
</template>

<script>
export default {
  name: 'Form',
  props: {},
  data: () => ({
    sourceSchema: null,
    targetSchema: null,
    equivalence: false,
    subsumption: false,
    valid: true,
    uploadFileRules: [
      value => !value || value.size < 2000000 || 'Maximum filesize is 2 MB!',
      value => value || 'File must be uploaded',
    ],
    dialog: false,
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
    checkboxRules () {
      return [
        () => this.equivalence || this.subsumption || 'Semantic relation is required'
      ]
    }
    
  },
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        this.$emit('submit', this.formData)
        this.dialog = true
      }
    },
  },
}
</script>

<style lang="scss">
  .rn-file-upload .v-input__slot {
    cursor: pointer!important;
  }
</style>
