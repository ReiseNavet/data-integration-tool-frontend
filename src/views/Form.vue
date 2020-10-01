<template>
  <div>
    <div class="row p-2">
      <div class="col">
        <v-file-input
          truncate-length="30" 
          placeholder="Source schema"
          show-size
          :rules="uploadFileRules"
          v-model="sourceSchema"
        />
      </div>
      <div class="col">
        <v-file-input
          truncate-length="30" 
          placeholder="Target schema"
          show-size
          :rules="uploadFileRules"
          v-model="targetSchema"
        />
      </div>
    </div>

    <div class="row p-2">
      <div class="col">
        <v-checkbox 
          v-model="equivalence"
          label="Equivalence"
        />
        <v-checkbox 
          v-model="subsumption"
          label="Subsumption"
        />
      </div>
    </div>

    <div class="row p-2">
      <div class="col">
        <button type="button" class="btn btn-primary" @click="submit">Compute Alignment</button>
      </div>
    </div>

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
    equivalence: true,
    subsumption: false,
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