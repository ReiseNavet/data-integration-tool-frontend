<template>
  <div>

    <v-data-table
      :headers="tableHeaders"
      :items="result"
      :items-per-page="10"
      class="elevation-1"
    />


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
    tableHeaders: [
      { text: 'Source', value: 'source' },
      { text: 'Target', value: 'target' },
      { text: 'Relation', value: 'relation' },
      { text: 'Confidence', value: 'confidence' },
    ],
  }),
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
