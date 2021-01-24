<template>
  <component :is="data.tag">
    {{ data.text }}
  </component>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      default: {
        text: {
          type: String,
          require: false
        },
        tag: {
          type: String,
          default: 'h1',
          require: true,
          validator(value) {
            return ['h1', 'h2', 'h3', 'h4', 'h5', 'h6','p'].includes(value)
          }
        }
      },
      require: true,
      validator(value) {
        return value.hasOwnProperty('tag')
      }
    },

  }
}
</script>

<style scoped>

</style>
