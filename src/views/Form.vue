<template>
  <div>
    <div class="row p-2">
      <div class="col input-group">
        <div class="custom-file">
          <label class="custom-file-label" for="source">Source Schema</label>
          <input class="custom-file-input" type="file" name="source" id="source">
        </div>
      </div>
      <div class="col input-group">
        <div class="custom-file">
          <label class="custom-file-label" for="target">Target Schema</label>
          <input class="custom-file-input" type="file" name="target" id="target">
        </div>
      </div>
    </div>

    <div class="row p-2">
      <div class="col">
        <label for="relations">Semantic Relations</label>
        <div class="form-check">
          <input class="form-check-input" type="checkbox" value="equivalence" id="equivalence" v-model="equivalence">
          <label class="form-check-label" for="equivalence"> Equivalence </label>
        </div>
        <div class="form-check">
          <input class="form-check-input" type="checkbox" value="subsumption" id="subsumption" v-model="subsumption">
          <label class="form-check-label" for="subsumption"> Subsumption </label>
        </div>
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
    sourceSchema: '',
    targetSchema: '',
    equivalence: false,
    subsumption: false,
    data: {},
  }),
  methods: {
    submit() {
      this.$emit('submit')
    },
  },
}
</script>

<style lang="scss">
</style>