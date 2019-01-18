<template>
  <svg xmlns="http://www.w3.org/2000/svg"
       :width="width"
       :height="height"
       viewBox="0 0 18 18"
  >
    <title :id="iconName">{{iconName}}icon </title>
    <g :fill="iconColor">
      <component :is="iconName"  />
    </g>
  </svg>
</template>

<script>
  import ArrowRightIcon from '~/components/icons/ArrowRightIcon'

  export default {
    name: 'app-icon',
    components: {
      ArrowRightIcon
    },
    props: {
      iconName: {
        type: String,
        required: true
      },
      width: {
        type: [Number, String],
        default: 20
      },
      height: {
        type: [Number, String],
        default: 20
      },
      iconColor: {
        type: String,
        default: 'currentColor'
      }
    }
  }
</script>

<style scoped>
</style>
