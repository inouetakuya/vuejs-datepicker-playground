<template>
  <div id="app">
    <h1>Datepicker Examples</h1>

    <div class="example">
      <h3>With minimum and maximum date range</h3>
      <datepicker :disabledDates="disabledDates"></datepicker>
      <code>
        &lt;datepicker :disabledDates="disabledDates"&gt;&lt;/datepicker&gt;
      </code>
      <div class="settings">
        <h5>Settings</h5>
        <pre>disabledDates: {{ disabledDates }}</pre>
        <h5>Resulting Date picker</h5>
        <datepicker :disabledDates="disabledDates"></datepicker>
      </div>
    </div>

    <div class="example">
      <div class="settings">
        <h5>Settings</h5>
        <div class="form-group">
          <label>Disabled Function:</label>
        </div>
        <pre>
          disabledDates: {
            customPredictor: function (date) {
              // disables every day of a month which is a multiple of 3
              if (date.getDate() % 3 === 0) {
                return true
              }
            }
          }
        </pre>
        <h5>Resulting Date picker</h5>
        <datepicker :disabledDates="disabledFn"></datepicker>
      </div>
    </div>
  </div>
</template>

<script>
import Datepicker from 'vuejs-datepicker/dist/vuejs-datepicker.esm.js'
import * as lang from 'vuejs-datepicker/src/locale'

const state = {
  date1: new Date()
}

export default {
  name: 'app',
  components: {
    Datepicker
  },
  data() {
    return {
      format: 'd MMMM yyyy',
      disabledDates: {
        ranges: [{
          from: new Date(1900, 0, 1),
          to: new Date(2021, 3, 30)
        }, {
          from: new Date(2021, 6, 1),
          to: new Date(2099, 11, 31)
        }]
      },
      disabledFn: {
        customPredictor(date) {
          if (new Date(2021, 4, 1) <= date && date <= new Date(2021, 6, 31)) {
            return false
          }
          return true
        }
      },
      highlightedFn: {
        customPredictor(date) {
          if (date.getDate() % 4 === 0) {
            return true
          }
        }
      },
      highlighted: {},
      eventMsg: null,
      state: state,
      language: 'en',
      languages: lang,
      vModelExample: null,
      changedMonthLog: []
    }
  },
}
</script>

<style>
body {
  font-family: "Helvetica Neue Light", Helvetica, sans-serif;
  padding: 1em 2em 2em;
}

input,
select {
  padding: 0.75em 0.5em;
  font-size: 100%;
  border: 1px solid #ccc;
  width: 100%;
}

select {
  height: 2.5em;
}

.example {
  background: #f2f2f2;
  border: 1px solid #ddd;
  padding: 0em 1em 1em;
  margin-bottom: 2em;
}

code,
pre {
  margin: 1em 0;
  padding: 1em;
  border: 1px solid #bbb;
  display: block;
  background: #ddd;
  border-radius: 3px;
}

.settings {
  margin: 2em 0;
  border-top: 1px solid #bbb;
  background: #eee;
}

h5 {
  font-size: 100%;
  padding: 0;
}

.form-group {
  margin-bottom: 1em;
}

.form-group label {
  font-size: 80%;
  display: block;
}
</style>
