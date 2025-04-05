<template>
  <q-page class="column">
      <h3> Add Notes</h3>

      <q-input
        v-model="text"
        placeholder="write something" 
        :dense="dense" 
        />
  <p>{{ text }}</p>
  </q-page>
</template>

<script>
  import { ref } from 'vue'
  export default {
   
    setup () {
     const text = ref('')


    return {
      text
    }
  }
  }
</script>

<style >


</style>