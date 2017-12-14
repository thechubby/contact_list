<template>
<div id="container">
  <div id="input">
    <input v-model="input_name" placeholder="Введите имя">
    <input v-model="input_phone" placeholder="Введите номер">
    <button type="button" class="btn btn-default" v-on:click="add">Добавить!</button>
  </div>

  <div id="app">
    <ul>
      <li v-for="contact in contacts">{{contact.name}}: {{contact.phone}}</li>
    </ul>
  </div>
</div>

</template>

<script>

export default {
  name: 'app',
  components: {
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
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
      ],
      input_name: '',
      input_phone: '',
    }
  },
  methods: {
    add: function () {
      this.contacts.push({
        name: this.input_name,
        phone: this.input_phone
      })
    }
  }
}
</script>

<style>
#container {
  border: 1px solid black;
  width: 500px;
  margin: auto;
}
#input {
  margin: 15px 0;
  text-align: center;
}

</style>
