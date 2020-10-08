<template>
  <div class="container">
   <v-row>
    <v-col>
      <h2>
        Alignment tool
      </h2>
    </v-col>
  </v-row>
  <v-row class="my-0">
    <v-col>
      <p>
          This alignment tool is used to compare two schemas. Upload both files, choose what semantic relation wanted and compute the alignment.
      </p>
    </v-col>
  </v-row>
  <v-container>
   <v-row class="my-0" justify="center">
      <h6>Upload files</h6>
  </v-row>
  <v-row class="my-0">
      <v-col>
        <v-file-input
          truncate-length="30" 
          placeholder="Source schema"
          show-size
          :rules="uploadFileRules"
          v-model="sourceSchema"
        />
      </v-col>
      <v-col>
        <v-file-input
          truncate-length="30" 
          placeholder="Target schema"
          show-size
          :rules="uploadFileRules"
          v-model="targetSchema"
        />
      </v-col>
    </v-row>
    <v-row class="my-0" justify="center">
      <h6>Choose semantic relation</h6>
    </v-row>
   <v-row class="my-0" justify="center">
        <v-checkbox 
          v-model="equivalence"
          label="Equivalence"
        />
    </v-row>
    <v-row class="my-0" justify="center">
        <v-checkbox 
          v-model="subsumption"
          label="Subsumption"
        />
    </v-row>
    <v-row class="my-0" justify="center">
        <v-btn
          color="orange"
          elevation="2"
          @click="submit"
        >   
        <v-icon dark>
          mdi-check
          </v-icon>
        Compute Alignment    
        </v-btn>
    </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'SchemaForm',
  props: {},
  data: () => ({
    uploadFileRules: [
      value => !value || value.size < 2000000 || 'Maximum filesize is 2 MB!'
    ],
    sourceSchema: null,
    targetSchema: null,
    equivalence: false,
    subsumption: false,
    alignments: [
        'center',
      ],
  }),
  computed: {
    formData() {
      return {
        sourceSchema: this.sourceSchema,
        targetSchema: this.targetSchema,
        equivalence: this.equivalence,
        subsumption: this.subsumption,
      }
    }
  },
  methods: {
    submit() {
      this.$emit('submit', this.formData)
    },
  },
}
</script>

<style lang="scss">

</style>
