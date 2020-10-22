<template>
  <div id="app">
    <button @click="fetchData()">
      Click me
    </button>

    {{ characters }}
  </div>
</template>

<script>
import { defineComponent, ref } from '@vue/composition-api'
import useAxios from './composables/useAxios'

export default defineComponent({
  name: 'App',
  setup () {
    const characters = ref(null)
    const { response, error, loading, exec } = useAxios()

    function fetchData () {
      exec({
        url: 'https://rickandmortyapi.com/api/character'
      })
        .then(() => {
          console.log(response.value)
          characters.value = response.value.data.results
        })
    }

    return {
      fetchData,
      characters,
      response,
      error,
      loading
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
