<template>
  <div class="form-control">
    <label for="custom-selector">{{ title }}</label>
    <select
      v-if="options.length"
      id="custom-selector"
      :selected="selected"
      @change="$emit('update:selected', $event.target.value)"
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
  emits: ['update:selected'],
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
  }
}
</script>

<style scoped>

</style>
