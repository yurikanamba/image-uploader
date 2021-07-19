<template>
  <h1>Upload images for Disposable Yurika</h1>     
  <UploadForm />
</template>
   
<script>
import UploadForm from './components/UploadForm.vue'

export default {
  name: 'App',
  components: {
    UploadForm
  }
}
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
