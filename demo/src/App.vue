<template>
  <div id="app">germogps
    <h1>vue-event-calendar</h1>
    <h2 class="t-center">Defaultgigearjgi r</h2>
    <vue-event-calendar
      :events="demoEvents"
      @day-changed="handleDayChanged"
      @month-changed="handleMonthChanged"
    ></vue-event-calendar>
    
    <h2 class="t-center mt150">Custom templatet</h2>
    <vue-event-calendar :events="demoEvents">
      <template scope="props">
        <div v-for="(event, index) in props.showEvents" class="event-item">
          <!-- In here do whatever you want, make you owner event template -->
          {{event}}
        </div>
      </template>
    </vue-event-calendar>
  </div>
</template>

<script>
let today = new Date()
export default {
  name: 'app',
  data () {
    return {
      demoEvents: [{
        date: `${today.getFullYear()}/${today.getMonth() + 1}/15`,
        title: 'Title-1',
        desc: 'longlonglong description',
        class: 'seppoC'
      },{
        date: `${today.getFullYear()}/${today.getMonth() + 1}/24`,
        title: 'Title-1211ð3',
        class: 'seppo'
      },{
        date: `${today.getFullYear()}/${today.getMonth() === 11 ? 1 : today.getMonth() + 2}/06`,
        title: 'Title-3',
        desc: 'description',
        class: 'seppo'
      }]
    }
  },
  methods: {
    handleDayChanged (data) {
      console.log('date-changed', data)
    },
    handleMonthChanged (data) {
      console.log('month-changed', data)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 30px;
}

h1, h2, h3 {
  font-weight: normal;
  margin: 0;
  padding: 0;
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
.t-center{
  text-align: center;
  margin: 20px;
}
.mt150{
  margin-top: 150px;
}
</style>
