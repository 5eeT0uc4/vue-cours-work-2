<template>
  <div class="container">
    <div v-if="!comments.length">
      <button class="btn primary" @click="$emit('load')">Загрузить комментарии</button>
    </div>
    <div v-else class="card" >
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="comment in comments" :key="comment.id">
          <div>
            <p><strong>{{ comment.email }}</strong></p>
            <small>{{ comment.body }}</small>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['load'],
  props: {
    comments: {
      type: Object,
      require: false,
      default: {}
    },
    loading: Boolean
  },
  data() {
    return {}
  },
  computed: {

  }
}
</script>

<style scoped>

</style>
