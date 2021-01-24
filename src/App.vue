<template>
  <div class="container column">
    <form class="card card-w30" @submit="submitHandler">

      <app-form-select
        title="Тип блока"
        :options="selector"
        :selected="selected"
        disabled="Выберите из списка"
        @action="selectorAction"
      ></app-form-select>

      <app-text-area
        title="Значение"
        placeholder="Введите значение"
        v-model:text="formValue"
      ></app-text-area>

      <app-button
        type="submit"
        :disabled="!checkFormValue"
      >Добавить
      </app-button>
    </form>

    <div class="card card-w70">
      <div v-for="(component, idx) in resume">
        <component
          :is="component.name"
          :key="idx"
          :data="component.data"
        ></component>
      </div>
    </div>
  </div>

  <app-comments-list
    :comments="comments"
    @load="loadComments"
  ></app-comments-list>

  <app-loader v-if="loading"></app-loader>

</template>

<script>

import AppTextArea from "./AppTextArea"
import AppFormSelect from "./AppFormSelect"
import AppButton from "./AppButton"
import AppAvatar from "./AppAvatar"
import AppText from "./AppText"
import AppCommentsList from "./AppCommentsList"
import AppLoader from './AppLoader'
import axios from "axios"

export default {
  components: {AppText, AppTextArea, AppFormSelect, AppButton, AppAvatar, AppCommentsList, AppLoader},
  data() {
    return {
      formValue: '',
      selected: 'header',
      resume: [],
      comments: [],
      loading: false,
      selector: [
        {value: 'header', text: 'Заголовок'},
        {value: 'subtitle', text: 'Подзаголовок'},
        {value: 'avatar', text: 'Аватар'},
        {value: 'text', text: 'Текст'}
      ],
      componentOptions: [
        {name: 'app-text', type: 'header', data: {tag: 'h1', text: ''}},
        {name: 'app-text', type: 'subtitle', data: {tag: 'h2', text: ''}},
        {name: 'app-avatar', type: 'avatar', data: {text: ''}},
        {name: 'app-text', type: 'text', data: {tag: 'p', text: ''}},
      ]
    }
  },
  methods: {
    submitHandler(event) {
      event.preventDefault()

      this.componentOptions.forEach(component => {
        const {type, data} = component
        if (type === this.selected) {
          data.text = this.formValue
          this.resume.push(JSON.parse(JSON.stringify(component)))
        }
      })

      this.clearForm()
    },
    selectorAction(value) {
      this.selected = value
    },
    clearForm() {
      this.selected = 'header'
      this.formValue = ''
    },
    async loadComments() {
      this.loading = true
      try {
        const {data} = await axios.get('https://jsonplaceholder.typicode.com/comments')
        if (!data) {
          throw new Error('Список комментариев пуст')
        }
        this.comments = data
        this.loading = false
      } catch (e) {
        this.loading = false
        console.log(e.message)
      }
    }
  },
  computed: {
    checkFormValue() {
      return this.formValue.length > 3
    }
  }
}
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
