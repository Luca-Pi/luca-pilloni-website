<template>
 <div>
   <slider :slides="slides" :titles="titles"/>
 </div>
</template>

<script>
  import Slider from "@/components/slider/slider";
  import slide1 from "@/components/digital-campus/project-test/slide1";
  import slide2 from "@/components/digital-campus/project-test/slide2";
  import slide3 from "@/components/digital-campus/project-test/slide3";
  import slide4 from "@/components/digital-campus/project-test/slide4";
  export default {
    name: "project-test",
    components: {Slider},
    data() {
      return {
        slides: [slide1, slide2, slide3, slide4],
        titles: ['Presentation', 'Renovation', 'Anticipation', 'Conclusion']
      }
    },
  }
</script>

<style lang="sass">
  @import "@/assets/sass/_variable.scss"
  h1
    color: $color-grey-dark-1

</style>
