<template>
  <div>
    <div class="row p-2">
      <div class="col">
        <table class="table table-striped">
          <thead class="table-borderless">
            <tr>
              <th scope="col">Source Schema</th>
              <th scope="col">Target Schema</th>
              <th scope="col">Relation</th>
              <th scope="col">Confidence</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="row in result" :key="row.source + row.target">
              <td>{{row.source}}</td>
              <td>{{row.target}}</td>
              <td>{{row.relation}}</td>
              <td>{{row.confidence.toFixed(2)}}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <div class="d-flex py-2">
      <div class="px-2">
        <button type="button" class="btn btn-primary" @click="download">Download alignment</button>
      </div>
      <div class="px-2">
        <button type="button" class="btn btn-primary" @click="reset">New alignment</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    result: {
      type: Array,
      required: true,
    }
  },
  data: () => ({

  }),
  computed: {
    filteredResult() {
      return this.result
    }
  },
  methods: {
    reset() {
      this.$emit('reset')
    },
    download() {
      // ref: https://stackoverflow.com/a/30800715/11192976
      const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(this.result, undefined, 2));
      const downloadAnchorNode = document.createElement('a');
      downloadAnchorNode.setAttribute("href",     dataStr);
      downloadAnchorNode.setAttribute("download", "result.json");
      document.body.appendChild(downloadAnchorNode); // required for firefox
      downloadAnchorNode.click();
      downloadAnchorNode.remove();
    }
  }

}
</script>

<style>

</style>