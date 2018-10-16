# Feathers Vuex Typeahead

Select component using feathers vuex services

## Important note

- You'll need feathers-vuex 1.7.0-pre.23 or greater in order to make this component work
- You'll need to setup your store first to prove the requiered service
- Limited to exact search by name only

### Steps

1. `npm i feathers-vuex@1.7.0-pre.23`
1. usually in `store/index.js` you add `service('your-service')`

## References

- [Feathers](https://feathersjs.com/)
- [Feathers-Vuex](https://github.com/feathers-plus/feathers-vuex)
- [Feathers-Vuex Docs](https://feathers-plus.github.io/v1/feathers-vuex/index.html)
- [Feathers-Vuex Mixins](https://feathers-plus.github.io/v1/feathers-vuex/mixins.html)

## Example


### Import and register in your VM:

```
import FeathersVuexSelect from 'feathers-vuex-typeahead'
...
export default {
  ...
  components: {
    FeathersVuexTypeahead
  },
  ...
}
```
 
### Use it in your template @TODO re-write
```
  <FeathersVuexTypeahead
    v-model="address.countryId"
    optionsValue="_id"
    optionsText="name"
    serviceName="country"
    :query="{ name: 'USA' }"
    optionsCaption="Select one country from the list"
    optionsSeparator=""
  />
```

## Params / properties  @TODO re-write
- **v-model**: wherever you want to store the selected option (`value/id`)
- **optionsValue**: property that defines the `id`
- **optionsText**: property that defines the text to show in the pull down (human readable)
- **serviceName**: name of the service, i.e. `/my-service`
- **:query**: an object with the query to get data from the service
- **optionsCaption**: if this is set (other than `""`) it will appear as a first option
- **optionsCaption**: if this is set (other than `""`) it will show a line before the available options (`------------------------------`)

