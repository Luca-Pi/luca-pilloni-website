<template>
  <div>
    <no-ssr>
      <vue-particles class="particles-container" color="#dedede"></vue-particles>
    </no-ssr>
    <header>
      <container3-d></container3-d>
    </header>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import AppAnimations from "../components/icons/AppAnimations";
import Popup3D from "../components/Popup3D";
import Container3D from "../components/Container3D";
export default {
  components: {
    Container3D,
    Popup3D,
    AppAnimations,
    Logo,

  },

}
</script>

<style lang="scss">
.particles-container {
  height: 100vh;
  width: 100vw;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}
header {
  padding: 10vw;
  padding-left: 15vw;
}
</style>
