<template>
  <div class="form-control">
    <label for="custom-selector">{{ title }}</label>
    <select
      id="custom-selector"
      v-model="selected"
      v-if="options.length"
    >
      <option v-if="disabled.length" disabled value="">{{ disabled }}</option>
      <option
        v-for="(option, i) in options"
        :value="option.value"
        :key="i"
      >
        {{ option.text }}
      </option>
    </select>
    <span v-else>Selector array is empty! Please define the options!</span>
  </div>
</template>

<script>
export default {
  emits: ['action'],
  props: {
    options: {
      type: Array,
      required: true,
      validator(options) {
        let value = true
        options.map(key => {
          if(!key.hasOwnProperty('text') || !key.hasOwnProperty('value')) {
            value = value && false
          }
        })

        return value
      }
    },
    title: {
      type: String,
      default: 'Selector'
    },
    disabled: {
      type: String,
      default: ''
    },
    selected: {
      type: String,
      required: false,
      default: '',
    }
  },
  watch: {
    selected(value) {
      this.$emit('action', value)
    }
  }
}
</script>

<style scoped>

</style>
