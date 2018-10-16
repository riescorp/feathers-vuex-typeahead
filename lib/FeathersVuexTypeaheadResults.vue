<template>
  <div>
    <div class="btn-group">
      <input v-model="queryText" @click="resetSelection" @input="resetSelection" v-on:blur="onBlur" v-on:keyup.enter="selectByIndex" v-on:keyup.esc="onBlur" v-on:keydown="keydown" /> Total: {{instanceArray.length}}<button @click="resetSelection" @tap="resetSelection">Start3</button> {{ indexSelected }}
      <ul v-if="instanceArray.length > 0" v-bind:style="{ display: showResults }" class="dropdown-menu feathers-vuex-typeahead-component">
        <li v-for="(instance, index) in instanceArray" v-bind:class="{ 'feathers-vuex-typeahead-selected-container': index === indexSelected }">
          <a v-on:click="setSelection(instance)">
            <FeathersVuexTypeaheadTemplate :instance="instance" v-bind:queryText="queryText" />
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import FeathersVuexTypeaheadTemplate from './FeathersVuexTypeaheadTemplate.vue'
export default {
  name: 'feathers-vuex-typeahead-results',
  props: ['instanceArray', 'value', 'optionsValue', 'optionsText', 'optionsCaption', 'serviceName', 'query', 'optionsSeparator', 'loading'],
  data () {
    return {
      queryText: '',
      queryId: '',
      showResultsVar: true,
      indexSelected: 0
    }
  },
  components: {
    FeathersVuexTypeaheadTemplate
  },
  computed: {
    showResults: function () {
      let out = 'none'
      if (this.showResultsVar) {
        if (this.queryText.length > 2 || this.queryText === '*') out = 'block'
      }
      return out
    }
  },
  methods: {
    setSelection: function (instance) {
      this.queryText = instance.name
      this.queryId = instance._id
      this.showResultsVar = false
      this.$emit('set-selection', instance._id)
    },
    onBlur: function (e) {
      console.log('>>> debug new feathers', this.instanceArray.length)
      // console.log('>>> debug new feathers', this)
      let self = this
      // workaround
      window.setTimeout(function () {
        self.showResultsVar = false
      }, 300)
      // this.showResultsVar = false // produce problemas
    },
    selectByIndex: function () {
      console.log('I need to select number', this.indexSelected)
      let indexSelected = this.indexSelected
      if (this.instanceArray && this.instanceArray.length > 0) {
        this.instanceArray.forEach((elem, index) => {
          if (index === indexSelected) this.setSelection(elem)
        })
      }
    },
    resetSelection: function () {
      this.showResultsVar = true
      this.indexSelected = 0
      // temporal
      this.$emit('updateSearch', this.queryText)
    },
    keydown: function (e) {
      this.$emit('updateSearch', this.queryText)
      this.showResultsVar = true
      if (e.code === 'ArrowDown') {
        console.log('>>> veifiying:', this.instanceArray.length)
        if (this.instanceArray && (this.instanceArray.length > (this.indexSelected + 1))) { this.indexSelected++ } // solo si no es el último
      } else if (e.code === 'ArrowUp') {
        if (this.indexSelected > 0) this.indexSelected-- // solo si no es el primero
      }
    }
  }
}
</script>
