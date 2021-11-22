<template>
      <div>
          <input type="checkbox" value="Percy" v-model="names">
          <label>Percy</label>
      </div>  
      <div>
          <input type="checkbox" value="Anabeth" v-model="names">
          <label>Anabeth</label>
      </div>  
      <div>
          <input type="checkbox" value="Nico" v-model="names">
          <label>Nico</label>
      </div>

      <p>Names: {{ names }}</p>
</template>

<script>
export default {
    data() {
        return {
            names: []
        }
    }
}
</script>

<style>

</style>