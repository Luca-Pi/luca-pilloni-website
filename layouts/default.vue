<template>
    <div>
      <navbar></navbar>
      <nuxt/>
    </div>
</template>

<script>

  import Navbar from "../components/ui/Navbar";
  export default {
    components: {Navbar}
  }
</script>
<style lang="sass">
  @import '@/assets/sass/main.sass'

</style>
