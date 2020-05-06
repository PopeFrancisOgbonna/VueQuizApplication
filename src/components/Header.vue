<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
    <b-navbar-brand href="#">
        <img src="../assets/logo.png" alt="">
        Quiz Application
    </b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
          <b-navbar-nav>
        <b-nav-item href="#" class="active">Home</b-nav-item>
        <b-nav-item href="#">Take Quiz</b-nav-item>
        <b-nav-item href="#" class="mr-md-4">About</b-nav-item>
      </b-navbar-nav>

        <b-nav-form>
          <b-form-input size="sm" class="mr-sm-2 ml-md-4" placeholder="Search"></b-form-input>
          <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
        </b-nav-form>

      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
  </div>
</template>

<script>
export default {
    name:'Header'
}
</script>

<style scoped>
    img{
        width: 48px;
        height: 48px;
        border:2px solid lightgreen;
        padding:10px;
        border-radius: 50%;
        background:#fff;
    }
</style>