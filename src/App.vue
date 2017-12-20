<template>
<div id="container">
  <div id="input" class="centerText marginVert">
      <input id="input_name" placeholder="ФИО">
      <input id="input_phone" placeholder="Контактные данные">
    <button type="button" class="btn btn-default" v-on:click="add()">Добавить</button>
  </div>

<div id="app">
  <ol>
    <li v-for="contact in contacts">
      {{contact.name}}: {{contact.phone}}
      <button type="button" class="btn btn-default" v-on:click="edit(contacts.indexOf(contact), refresh())">Обновить</button>
      <button type="button" class="btn btn-default" v-on:click="del(contacts.indexOf(contact))">Удалить</button>
    </li>
    </ol>
    <div class="centerText marginVert">
      <button type="button" class="btn btn-default" v-on:click="store()">Сохранить книгу</button>
  </div>
</div>

  <div id='description' class="centerText marginVert">
    <p>Для добавления записи введите данные и нажмите "Добавить"<br>
    Для редактирования записи введите данные и нажмите "Обновить"<br>
    Для сохранения изменений в книге нажмите "Сохранить книгу"</p>
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
      contacts: JSON.parse(localStorage.getItem('key')) //выгружаем из локального хранилища последний сейв, если он был
    }
  },
  methods: {

    store: function() {
      let conts = JSON.stringify(this.contacts);
      localStorage.setItem('key', conts);
    }, //сохраняем в локальное хранилище текущее состояние книги

    refresh: function() {
      this.contacts.push({})
      this.contacts.pop()
    }, //костыль для повторного рендера v-for т.к. v-for не реагирует на изменение эл-в массива, а только на изменение кол-ва эл-в

    add: function () {
      this.contacts.push({
        name: document.getElementById('input_name').value,
        phone: document.getElementById('input_phone').value
      })
    },

    edit: function(contact) {
        this.contacts[contact] = {
          name: document.getElementById('input_name').value,
          phone: document.getElementById('input_phone').value
      }
    },

    del: function(contact) {
      this.contacts.splice(contact,1)
    }
  }
}
</script>

<style>
#container {
  font-family: 'Spectral SC', serif;
  border: 1px solid black;
  margin: auto;
  width: 500px;
  font-family: 'Lobster', cursive;  
}
#description{
  line-height: 22px;
}

.centerText {
  text-align: center;
}
.marginVert {
  margin: 15px 0px;
}

ol {
  border-bottom: 1px solid black;
  border-top: 1px solid black;
  padding-top: 15px;
  padding-bottom: 15px;
}
li {
  line-height: 40px;
}
/*Ширины для десктопов*/
@media screen and (device-width: 1920px) {
  #container {width: 1440px;}
}
@media screen and (device-width: 1440px) {
  #container {width: 960px;
  }
@media screen and (device-width: 1280px) {
  #container {width: 768px;}
}
@media screen and (device-width: 1024px) {
  #container {width: 600px;}
}
@media screen and (device-width: 800px) {
  #container {width: 500px;}
}
/*Для мобильных*/
@media screen and (max-width: 480px) {
    #container {
      width: 480px;
    }
    font-size: 10px;
  }
}
</style>
