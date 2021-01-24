<template>
  <div class="form-control">
    <label for="value">{{ title }}</label>
    <textarea
      id="value"
      :rows="rows"
      :placeholder="placeholder"
      :value="text"
      @input="$emit('update:text', $event.target.value)"
    ></textarea>
  </div>
</template>

<script>
export default {
  emits:['update:text'],
  props: {
    text: String,
    placeholder: {
      type: String,
      required: false,
      default: ''
    },
    rows: {
      type: Number,
      required: false,
      default: 3
    },
    title: {
      type: String,
      required: false,
      default: ''
    }
  }
}
</script>

<style scoped>

</style>
