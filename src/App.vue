<template>
  <div id="app">
    <input v-model="newContact" @keydown.enter="addContact" placeholder="Enter new contact - phone number"/>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      newContact: '',
      contacts: []
    }
  },
  methods: {
    addContact () {
      this.contacts.push(this.newContact)
      this.newContact = ''
      console.log('contact list: ', this.contacts)
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  input {
    padding: 10px 15px;
  }
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
