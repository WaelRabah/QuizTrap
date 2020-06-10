<template>
  <div>
      <b-nav tabs>
      <b-nav-item disabled><b>Quiz App</b></b-nav-item>
      <b-nav-item disabled>Counter : {{this.score +"/10"}}</b-nav-item>
      <b-nav-item disabled>Category : {{this.category}}</b-nav-item>
        </b-nav>
  </div>
</template>

<script>
export default {
    name :'Header',
    props : ["score","category"]
}
</script>

<style>

</style>