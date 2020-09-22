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

    <hr class="mx-2">

    <div class="row px-2">
      <div class="col form-group">
        <label for="text">Example text-field <span class="text-muted">(To show how v-model works in vue)</span></label>
        <input class="form-control" type="text" id="text" v-model="text">
      </div>
    </div>

    <div class="row px-2">
      <div class="col">
        <p><span class="font-weight-bold text-muted">Text field value:</span> {{text}}</p>
      </div>
    </div>

    <hr class="mx-2">

    <div class="row p-2">
      <div class="col">
        <button type="button" class="btn btn-primary my-2" @click="fetchData">Fetch from API</button>
        <div class="card bg-dark p-2">
          <pre class="text-white">{{dataJson}}</pre>
        </div>
      </div>
    </div>

    <hr class="mx-2">

    <div class="row p-2">
      <div class="col">
        <label for="relations">Semantic Relations</label>
        <div class="form-check">
          <input class="form-check-input" type="checkbox" value="equivalence" id="equivalence" v-model="relations">
          <label class="form-check-label" for="equivalence"> Equivalence <span v-if="eqChecked">CHECKED</span></label>
        </div>
        <div class="form-check">
          <input class="form-check-input" type="checkbox" value="subsumption" id="subsumption" v-model="relations">
          <label class="form-check-label" for="subsumption"> Subsumption <span v-if="subChecked">CHECKED</span></label>
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
    text: '',
    relations: [],
    data: {},
  }),
  methods: {
    submit() {
      console.log(this.sourceSchema, this.targetSchema, this.relations)
    },
    async fetchData() {
      if(process.env.NODE_ENV === 'production') {
        // Localhost-api doesn't work in production.
        console.warn("Hey, the server isn't running in production yet, so you'll have to run it locally with the backend.")
        this.data = "This doesn't work online yet. Try locally."
        return
      }
      const response = await fetch('http://localhost:7000')
      this.data = await response.json()
      console.log(this.data)
    },
  },
  computed: {
    eqChecked() {
      return this.relations.includes('equivalence')
    },
    subChecked() {
      return this.relations.includes('subsumption')
    },
    dataJson() {
      return JSON.stringify(this.data)
    }
  }
}
</script>

<style lang="scss">
</style>
