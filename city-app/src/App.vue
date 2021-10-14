<template>
  <div id="app">
    <Login></Login>
  </div>
</template>

<script>
import Login from './components/login'
export default {
  name: 'App',
  components: {
   Login
  }
}
</script>

<style>
#app {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-family: 'Courier New', Courier, monospace;

}
</style>
