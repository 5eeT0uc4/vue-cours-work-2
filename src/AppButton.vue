<template>
  <div>
    <button
      class="btn"
      :disabled="disabled"
      :class="color"
      @click="$emit('action')"
    >
      <slot />
    </button>
  </div>
</template>

<script>
export default {
  emits: ['action'],
  props: {
    disabled: false,
    color: {
      type: String,
      default: '',
      validator(value) {
        return ['', 'primary', 'danger'].includes(value)
      }
    }
  }
}
</script>

<style scoped>

</style>
