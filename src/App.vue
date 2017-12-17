<template>
<div id="container">
  <div id="input" class="centerText marginVert">
    <input v-model="input_name" placeholder="Введите имя">
    <input v-model="input_phone" placeholder="Введите номер">
    <button type="button" class="btn btn-default" v-on:click="add">Добавить!</button>
  </div>

  <div id="app">
    <ul>
      <li v-for="contact in contacts">{{contact.name}}: {{contact.phone}} <button type="button" class="btn btn-default" v-on:click="edit(contacts.indexOf(contact))">Обновить!</button></li>
    </ul>
  </div>
  <div id='description' class="centerText marginVert">
    <p>Для добавления записи введите данные и нажмите "Добавить!"<br>Для редактирования записи введите данные и нажмите "Обновить!"</p>
  </div>
</div>

</template>

<script>
import _ from 'lodash';

export default {
  name: 'app',
  components: {
  },
  data () {
    return {
      contacts: [
        {  
          name: 'Иванов Иван',
          phone: '+7 999 888 77 66'
        },
        {
          name: 'Гуси Лебеди',
          phone: '+7 123 456 78 90'
        },
        {
          name: 'Петров Петр',
          phone: '+7 987 654 32 10'
        },
        {
          name: 'Васильев Василий',
          phone: '+7 999 888 77 66'
        }
      ]
    }
  },
  methods: {
    add: function () {
      this.contacts.push({
        name: this.input_name,
        phone: this.input_phone
      })
    },
    edit: function(contact) {
        this.contacts[contact] = {
          name: this.input_name,
          phone: this.input_phone
      } //Создаем и сразу же удаляем последний эл-т массива для повторного рендеринга v-for
        this.contacts.push({})
        this.contacts.pop()
    }
  },
  watch: {
    
  }
}
</script>

<style>
#container {
  border: 1px solid black;
  width: 500px;
  margin: auto;
}
.centerText {
  text-align: center;
}
.marginVert {
  margin: 15px 0px;
}
ul {
  border-bottom: 1px solid black;
  border-top: 1px solid black;
  padding-top: 15px;
  padding-bottom: 15px;
}
</style>
