<template>
  <div @wheel="scroll" @keyup.up="scroll"
       class="container"
       v-touch="{
        up: () => updateCurrent('down'),
        down: () => updateCurrent('up')
       }"
  >
    <div class="slider">
      <div class="slider__nav">
        <button
          v-for="(title, i) in titles"
          class="slider__nav__btn slider__nav__btn--green"
          :class="{'btn-focused': current === i}"
          @click="goTo(i)"
          :key="i"
        >
          <span>{{title}}</span>
        </button>
      </div>
        <component
          v-for="(slide, i) in slides"
          :is="slide"
          :key="i" :class="'slider__slide slide--'+i"
          :ref="'slide'+i"
          :isCurrent="isCurrent[i]"
        />
    </div>
  </div>
</template>

<script>
  import anime from 'animejs'
  import AppIcons from "../icons/AppIcons";

  export default {
    name: "slider",
    components: {AppIcons},
    props: {
      slides: Array,
      titles: Array,
    },
    data() {
      return {
        oldCurrent: 0,
        current: 0,
        isCurrent: [],
        disabled: false
      }
    },
    created() {
      this.slides.forEach((item, i) => {
        this.isCurrent[i] = false;
      });
    },
    beforeMount() {
      window.addEventListener('keyup', (event) => {
        console.log(event);
        if (event.key === 'ArrowUp') this.updateCurrent('up');
        if (event.key === 'ArrowDown') this.updateCurrent('down');

        if (event.key === ' ') this.updateCurrent('down');
      });

    },
    mounted() {
      this.isCurrent[0] = true;
    },
    beforeDestroy() {
      window.removeEventListener('keyup', null);
    },
    methods: {
      scroll(e){
        if(e.deltaY < 0) {
          this.updateCurrent('up')
        } else {
          this.updateCurrent('down')
        }
      },
      updateCurrent(e) {
        if(this.disabled) return;

        if(e === 'up') {

          this.current = this.current > 0 ? this.current - 1 : this.current;

        } else if (e === 'down') {

          this.current = this.current < this.slides.length - 1 ? this.current + 1 : this.current;

        }
        this.disabled = true;
        setTimeout(() => {
          this.disabled = false
        }, 1500);
        this.slide();
      },
      goTo(i) {
        if(i === this.current) return;
        this.current = i;
        this.slide();
      },
      slide() {

      }
    },
    watch: {
      current(newValue, oldValue) {
        this.isCurrent[oldValue] = false;

        const slideAnime = anime({
          targets: '#slider',
          translateY: -95 * this.current + 'vh',
          easing: 'easeInOutQuart'
        });
        slideAnime.finished.then(() => {
          this.$set(this.isCurrent, newValue, true);
          console.log(this.isCurrent, this.current);
        })
      }
    }
  }
</script>

<style scoped lang="sass">

  .container
    position: absolute
    overflow: hidden
    display: block
    left: 60px
    width: 100%
    max-width: 100%
    height: 100%
    margin: 0
    padding: 0

  .slider
    &__slide
      height: 100vh
    &__nav
      position: absolute
      top: 1rem
      left: 1rem
      display: flex
      margin: 2rem
      z-index: 10

      &__btn
        &,
        &:link,
        &:visited
          text-transform: uppercase
          text-decoration: none
          padding: 1.5rem 4rem
          margin-right: .5rem
          display: inline-block
          border-radius: .2rem
          transition: all .2s
          position: relative
          font-size: 1.6rem
          border: none
          cursor: pointer
          transform: skew(-21deg)

        &:hover
          transform: translateY(-3px) skew(-21deg)
          box-shadow: 0 1rem 2rem rgba(black,.2)

          &::after
            transform: scaleX(1.4) scaleY(1.6) skew(-21deg)
            opacity: 0

        &:active,
        &:focus
          outline: none
          transform: translateY(-2px) skew(-21deg)
          box-shadow: 0 .5rem 1rem rgba(black,.2)

        span
          transform: skew(21deg)
          display: inline-block

        &::after
          content: ""
          display: inline-block
          height: 100%
          width: 100%
          border-radius: .5rem
          position: absolute
          top: 0
          left: 0
          z-index: -1
          transition: all .4s

        &--green
          background: #55C57A
          color: white

          &::after
            background: #55C57A


  .btn-focused
    outline: none
    transform: translateY(-2px) skew(-21deg)
    box-shadow: 0 .5rem 1rem rgba(black,.2)


</style>
