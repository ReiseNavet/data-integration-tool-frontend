<template>
  <div class="example-container">
    <SchemaForm :dynamicValue="stateVariable" @click="incrementStateVariable"/>
    <p class="text-muted">{{propNumberOne}}</p>
  </div>
</template>

<script>
import SchemaForm from './SchemaForm'
export default {
  name: 'DefaultComponent',
  components: { SchemaForm },
  props: {
    propNumberOne: {
      type: String,
      required: false,
      default: "My default prop value",
    }
  },
  data: () => ({
    stateVariable: 42,
    externalData: null,
  }),
  computed: {
    stateVariableGreaterThan40() {
      return this.stateVariable > 40
    },
  },
  methods: {
    incrementStateVariable(value) {
      this.stateVariable += value
      this.$emit('customEvent', value)
    },
    async fetchData() {
      const response = await fetch('http://example.com/api')
      this.externalData = await response.json()
    },
  },
}
</script>

<style lang="scss">
 .example-container {
   color: red;
 }
</style>