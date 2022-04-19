<template>
<div class="container">
  <div align="center">
    <FormUsuario/>
  </div>
</div>
</template>
<script>
import FormUsuario from '../components/FormUsuario';
export default {
  components: { FormUsuario },
  name: 'nuevoadmin',
  layout: 'principal'
};
</script>