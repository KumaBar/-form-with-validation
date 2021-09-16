<template>
  <div id="app">
<Form/>
  </div>
</template>

<script>
import Form from  './views/Form'
export default {
  name: 'App',
  components: {
    Form
  }
}
</script>

<style>
body{
  background:lightgrey;
  min-height:100vh;
  padding:0;
  margin:0;
  font-family: 'Roboto', sans-serif;
}
#app{
  min-height:100vh;
}
</style>
