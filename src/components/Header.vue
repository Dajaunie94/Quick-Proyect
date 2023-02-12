<template>
<div>
  <b-navbar type="dark" variant="dark">
    <b-navbar-nav>
      <b-nav-item href="/dashboard"><img src="@/assets/log.png" id="icon" alt="User Icon" /></b-nav-item>

      <b-navbar-nav>
        <b-nav-item href="/dashboard">Tabla</b-nav-item>
        <b-nav-item href="/characteristics" >Caracteristicas</b-nav-item>
      </b-navbar-nav>

      <b-nav-item-dropdown text="Administrador" align="left">
        <b-dropdown-item href="/">Salir</b-dropdown-item>
        
      </b-nav-item-dropdown>
    </b-navbar-nav>
  </b-navbar>

    <br><br>
</div>
</template>

<script>
// @ is an alias to /src


export default {
  name: 'Header',
  components: {
   
  },
  methods:{
    inicio(){
        this.$router.push('/');
    }
  }
}
</script>

<style scoped>



</style>