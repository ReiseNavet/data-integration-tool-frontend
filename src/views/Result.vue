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
            <tr>
              <td>Planned departure</td>
              <td>Scheduled departure</td>
              <td>=</td>
              <td>0.8</td>
            </tr>
            <tr>
              <td>Stop point</td>
              <td>Bus stop</td>
              <td>&gt;</td>
              <td>0.9</td>
            </tr>
            <tr>
              <td>Stop point</td>
              <td>Location</td>
              <td>&lt;</td>
              <td>0.75</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <div class="row p-2">
      <div>
        <button type="button" class="btn btn-primary">Download alignment</button>
      </div>
      <div>
        <button type="button" class="btn btn-primary">New allignment</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>