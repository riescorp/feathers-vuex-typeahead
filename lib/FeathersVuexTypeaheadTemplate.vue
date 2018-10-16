<template>
  <div class="feathers-vuex-typeahead-container">
    <!-- <span>{{ instance.name }}</span> | -->
    <!-- <span>{{ instance._id }}</span> | -->
    <span v-html="highlightedText"></span>
  </div>
</template>
<script>
export default {
  name: 'feathers-vuex-typeahead-template',
  props: ['instance', 'queryText'],
  data () {
    return {
      highlightTag: 'span',
      highlightClasses: 'feathers-vuex-typeahead-highlight',
      mainProperty: 'name'
    }
  },
  computed: {
    highlightedText: function () {
      let needle = this.queryText
      let haystack = this.instance[this.mainProperty]
      if (needle !== '*') {
        let regularExpression = new RegExp(`(${needle})`, 'i')
        if (regularExpression.test(haystack)) {
          return haystack.replace(regularExpression, `<${this.highlightTag} class="${this.highlightClasses}">$1</${this.highlightTag}>`)
        } else {
          return haystack
        }
      } else {
        return haystack
      }
    }
  }
}
</script>
<style>
.feathers-vuex-typeahead-selected-container {
  background: teal;
  /*color: white;*/
}

.feathers-vuex-typeahead-selected-content {
  color: white;
}

.feathers-vuex-typeahead-container {
  /*color: red;*/
}

.feathers-vuex-typeahead-highlight {
  background: yellow;
  color: #333;
  font-weight: 600;
}

.feathers-vuex-typeahead-highlight:hover {
  /*background: purple !important;*/
  /*color: #333;*/
}
</style>
