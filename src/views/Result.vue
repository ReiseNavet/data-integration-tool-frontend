<template>
<div class="container">
  <v-row>
    <v-col>
      <h2> Alignment result </h2>
    </v-col>
    <v-col>
      <v-row>
        <v-col>
          <v-btn color="white" elevation="2" @click="download">    
            <v-icon dark> mdi-download </v-icon>
            Download alignment 
          </v-btn>
        </v-col>
        <v-col>
          <v-dialog v-model="dialog" persistent max-width="290">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="orange" v-bind="attrs" v-on="on">
                <v-icon dark> mdi-arrow-left </v-icon>
                New alignment
              </v-btn>
            </template>
            <v-card>
              <v-card-title class="headline">
                Go back?
              </v-card-title>
              <v-card-text> When going back to make a new alignment the results will be deleted.</v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="white" @click="reset" >
                  <v-icon dark> mdi-arrow-left </v-icon>
                  Ok
                </v-btn>
                <v-btn color="orange" @click="dialog = false" >
                  <v-icon dark> mdi-cancel </v-icon>
                  Cancel
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-col>
      </v-row>
    </v-col>
  </v-row>
  <v-row justify="center">
    <v-col>
      <p> The results are presented in the table. You can download the alignment results as a <code>.json</code>-file. </p>
    </v-col>
  </v-row>
  <v-row>
    <v-col>
      <v-data-table
      :headers="tableHeaders"
      :items="result"
      :items-per-page="10"
      class="elevation-1"
    />
    </v-col>
  </v-row>
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
    dialog: false,
    justify: [
        'space-between',
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
