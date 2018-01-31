<template>
    <div id="app">
        <div class="wrapper">
            <input class="add-contact" v-model="newContact" @keydown.enter="addContact" placeholder="Enter new contact - phone number"/>

            <div class="listing-wrapper">
                <ul class="listing">
                    <li v-for="(item, index) in contacts" :class="{ completed: item.completed }">
                        <input type="checkbox" v-model="item.completed">
                        {{ item.text }}
                    </li>
                </ul>
            </div>
        </div>
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
        this.contacts.push({
          text: this.newContact,
          completed: false
        })
        this.newContact = ''
        console.log('contact list: ', this.contacts)
      }
    },
    watch: {
      contacts: {
        handler() {
          console.log('Contacts seems to have changed!');
        },
        deep: true, // this directs Vue to look at all nested properties inside the array
      },
    },
    mounted () {
      console.log('App loaded')
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
            &.add-contact {
                width: 100%;
                max-width: 350px;
                padding: 10px 15px;
                margin: 0px 20px;
            }
        }

        div {
            &.listing-wrapper {
                width: 100%;
                max-width: 400px;
                margin: 0px auto;
            }
        }

        ul {
            li {
                display: block;
                line-height: 45px;
                text-align: left;
            }
        }
    }

    .completed {
        text-decoration: line-through;
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
