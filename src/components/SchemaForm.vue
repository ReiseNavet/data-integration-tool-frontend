<template>
  <div>
    <div class="row p-2">
      <div class="col form-group">
        <label for="source">Source Schema</label>
        <input class="form-control" type="text" name="source" v-model="sourceSchema">
      </div>
      <div class="col form-group">
        <label for="target">Target Schema</label>
        <input class="form-control" type="text" name="target" v-model="targetSchema">
      </div>
    </div>

    <div class="row p-2">
      <div class="col">
        <label for="relations">Semantic Relations</label>
        <div class="form-check">
          <input class="form-check-input" type="checkbox" value="equivalence" id="equivalence" v-model="relations">
          <label class="form-check-label" for="equivalence"> Equivalence </label>
        </div>
        <div class="form-check">
          <input class="form-check-input" type="checkbox" value="subsumption" id="subsumption" v-model="relations">
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
    relations: [],
  }),
  methods: {
    submit() {
      console.log(this.sourceSchema, this.targetSchema, this.relations)
    }
  }
}
</script>

<style lang="scss">
</style>
