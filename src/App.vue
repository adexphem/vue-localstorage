<template>
    <div id="app">
        <div class="title">Simple usage - localStorage <span class="counter">{{ counter || 0 }}</span></div>
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
        contacts: [],
        counter: ''
      }
    },
    methods: {
      addContact () {
        this.contacts.push({
          text: this.newContact,
          completed: false
        })
        this.newContact = ''
        this.counter = this.getCount()
      },
      getCount () {
        return this.contacts.length
      }
    },
    watch: {
      contacts: {
        handler() {
          // Contacts seems to have changed now
          localStorage.setItem('appContacts', JSON.stringify(this.contacts))
        },
        deep: true, // this directs Vue to look at all nested properties inside the array
      },
    },
    mounted () {
      // App is loaded at this point
      if (localStorage.getItem('appContacts')) {
        this.contacts = JSON.parse(localStorage.getItem('appContacts'))
        this.counter = this.getCount()
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

        .title {
            font-weight: 600;
            font-size: 28px;
            text-align: center;
            line-height: 45px;

            span {
                font-size: 10px;
                font-weight: 900;
                display: inline-block;
                vertical-align: middle;
                border-radius: 50%;
                border: .5px solid rgba(220, 237, 254, .8);
                width: 20px;
                height: 20px;
                line-height: 20px;
                color: #0879EA;
            }
        }

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
