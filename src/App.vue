<template>
  <div id="app" class="container-sm px-lg-5">
    <div class="row py-2">
      <div class="col px-2">
        <div class="card">
          <SchemaForm/>
        </div>
      </div>
      <div class="col px-2">
        <div class="card">
          <ComputedAlignment/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SchemaForm from './components/SchemaForm'
import ComputedAlignment from './components/ComputedAlignment'
export default {
  name: 'App',
  components: {
    SchemaForm, 
    ComputedAlignment,
  }
}
</script>
