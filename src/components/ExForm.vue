<template>
  <div>
    <div class="section">
      <div class="field">
        <label for="entry" class="label">Random Input</label>
        <input class="input" type="text" :placeholder="placeheld" v-model="inputted">
      </div>
      <div class="field">
        <label class="label">Subject</label>
        <div class="control">
          <div class="select">
            <select v-model="selected">
              <option value="">Make a selection</option>
              <option v-for="(option, index) in options" :key="`opt-${index}`"  :value="option.value">
                {{option.text}}
              </option>
            </select>
          </div>
        </div>
      </div>
      <div class="field">
        <div class="control">
          <label class="label">POST into the ether?</label>
          <label class="radio">
            <input type="radio" name="question" v-model="mode" value="remote" @click="resetSubmit">
            Yes
          </label>
          <label class="radio">
            <input type="radio" name="question" v-model="mode" value="local" @click="resetSubmit">
            No
          </label>
        </div>
      </div>
      <div class="field is-grouped">
        <div class="control">
          <button class="button is-link" @click="submit">Submit</button>
        </div>
        <div class="control">
          <button class="button is-text" @click="cancel">Cancel</button>
        </div>
      </div>
    </div>
    <div class="section" v-if="mode === 'local' && submitted">
      <ul>
        <li><b>Random Input</b> {{inputted}}</li>
        <li><b>Subject</b> {{selected}}</li>
        <li><b>POST?</b> {{mode}}</li>
      </ul>
    </div>
    <div class="section" v-if="mode === 'remote' && submitted">
      <ul>
        <li><b>Data posted remotely to {{api}}</b> <pre>{{postData}}</pre></li>
        <li><b>POST?</b> {{mode}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ExForm',
  data () {
    return {
      api: 'http://jsonplaceholder.typicode.com',
      postData: null,
      submitted: false,
      mode: 'local',
      inputted: '',
      placeheld: 'I am a placeholder',
      selected: '',
      options: [
        { text: 'Selection A', value: 'A' },
        { text: 'Selection B', value: 'B' },
        { text: 'Selection C', value: 'C' },
        { text: 'Selection D', value: 'D' },
        { text: 'Selection E', value: 'E' }
      ]
    }
  },
  computed: {
    datum () {
      return {
        input: this.inputted,
        selection: this.selected
      }
    }
  },
  methods: {
    async submit () {
      this.submitted = true
      if (this.mode === 'remote') {
        const response = await this.axios.post(`${this.api}/posts`, this.datum)
        this.postData = await response.data
      }
    },
    resetSubmit () {
      this.submitted = false
    },
    clear () {
      this.mode = 'local'
      this.inputted = ''
      this.selected = ''
      this.submitted = false
    },
    cancel () {
      this.clear()
    }
  },
  created () {
    // this.selected = this.options[0].value
  }
}
</script>

<style>
</style>
