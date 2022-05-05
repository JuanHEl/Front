<template>
  <div class="container">
    <div class="logo">
    </div>
    <div class=" login">
      <FormLogin/>
    </div>
  </div>
</template>

<script>
import FormLogin from '../components/FormLogin.vue'
export default {
  name: 'login',
  layout: 'default',
  component: {FormLogin}
};
</script>

<style scoped>
.logo{
  width: 60%;
  height: 100%;
}
.login{
  width: 30%;
  padding: 0;
  margin: 0;
}
.container{
  display: flex;
}
</style>
