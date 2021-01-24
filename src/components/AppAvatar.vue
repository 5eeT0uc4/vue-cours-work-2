<template>
  <div class="avatar">
    <img :src="data.text" alt="Avatar">
  </div>
</template>

<script>
export default {
  props: {
    data: {
      text: {
        type: String,
        required: true,
        validator(value) {
          return this.isValidUrl(value)
        }
      }
    }

  },
  methods: {
    isValidUrl(string) {
      const res = string.match(/(http(s)?:\/\/.)?(www\.)?[-a-zA-Z0-9@:%._+~#=]{2,256}\.[a-z]{2,6}\b([-a-zA-Z0-9@:%_+.~#?&/=]*)/g);
      return (res !== null)
    }
  }
}
</script>

<style>

</style>
