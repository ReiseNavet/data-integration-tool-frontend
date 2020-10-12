<template>
  <v-container>
    <v-row>
      <v-col>
        <h2> Alignment tool </h2>
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
    <v-row class="my-0" justify="center">
      <h6>Upload files</h6>
    </v-row>
    <v-row class="my-0 rn-file-upload">
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
        @click="submit"
      >   
      <v-icon dark>
        mdi-check
        </v-icon>
      Compute Alignment    
      </v-btn>
    </v-row>
  </v-container>
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
  .rn-file-upload .v-input__slot {
    cursor: pointer!important;
  }

  // .rn-checkboxes .v-messages {
  //   height: 0!important;
  //   min-height: 0!important;
  //   padding: 0!important;
  // }
</style>
