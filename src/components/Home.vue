<template>
  <div class="home section">
    <div class="container">
      <h1 class="title">Form</h1>
      <ex-form></ex-form>
    </div>
  </div>
</template>

<script>
import ExForm from './ExForm'
export default {
  name: 'Home',
  components: {
    'ex-form': ExForm
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
