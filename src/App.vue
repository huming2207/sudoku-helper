<template>
  <div id="app">
    <Sudoku />
  </div>
</template>

<script>
import Sudoku from './components/Sudoku.vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default {
  name: 'app',
  components: {
    Sudoku
  }
}
</script>
