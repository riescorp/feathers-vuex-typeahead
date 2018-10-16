<template>
  <div>
    <FeathersVuexTypeaheadResults
      v-bind:value="value"
      v-on:set-selection="setSelection"
      v-bind:instanceArray="country"
      v-on:updateSearch="updateSearch"
      watch="country" />
  </div>
</template>
<script>
import { makeFindMixin } from 'feathers-vuex'
console.log('>>> checkpoint', makeFindMixin)
import FeathersVuexTypeaheadResults from './FeathersVuexTypeaheadResults.vue'
export default {
  name: 'feathers-vuex-typeahead',
  props: ['value', 'serviceName', 'query'],
  data () {
    return { queryText: '' }
  },
  mixins: [
    makeFindMixin({ service: 'country', query: 'queryObject' })
  ],
  components: { FeathersVuexTypeaheadResults },
  computed: {
    queryObject: function () {
      let query = { name: this.queryText }
      if (this.queryText === '*' || this.queryText === '') query = {}
      return query
    },
    todosQuery () {
      return {}
    }
  },
  methods: {
    updateSearch: function (text) {
      this.queryText = text
    },
    setSelection: function (_id) {
      this.$emit('done', _id)
    },
    some: function () {
      return 'country'
    }
  }
}
</script>

