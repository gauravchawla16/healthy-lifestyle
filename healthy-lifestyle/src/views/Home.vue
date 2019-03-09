<template>
  <div>
    <el-autocomplete
  v-model="state4"
  :fetch-suggestions="querySearchAsync"
  placeholder="Please input"
  @select="handleSelect"
></el-autocomplete>
<component-detail :item="item"></component-detail>
  </div>
</template>

<script>
// @ is an alias to /src
import { Autocomplete } from 'element-ui'
import ComponentDetail from '@/components/ComponentDetail.vue'

export default {
  name: 'home',
  components: {
    ComponentDetail,
    'el-autocomplete': Autocomplete
  },
  data () {
    return {
      links: [],
      state4: '',
      timeout: null,
      item: {}
    }
  },
  methods: {
    loadAll () {
      return [
        { 'value': 'vue', 'link': 'https://github.com/vuejs/vue' },
        { 'value': 'element', 'link': 'https://github.com/ElemeFE/element' },
        { 'value': 'cooking', 'link': 'https://github.com/ElemeFE/cooking' },
        { 'value': 'mint-ui', 'link': 'https://github.com/ElemeFE/mint-ui' },
        { 'value': 'vuex', 'link': 'https://github.com/vuejs/vuex' },
        { 'value': 'vue-router', 'link': 'https://github.com/vuejs/vue-router' },
        { 'value': 'babel', 'link': 'https://github.com/babel/babel' }
      ]
    },
    querySearchAsync (queryString, cb) {
      var links = this.links
      var results = queryString ? links.filter(this.createFilter(queryString)) : links

      clearTimeout(this.timeout)
      this.timeout = setTimeout(() => {
        cb(results)
      }, 3000 * Math.random())
    },
    createFilter (queryString) {
      return (link) => {
        return (link.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0)
      }
    },
    handleSelect (item) {
      console.log(item)
    }
  },
  mounted () {
    this.links = this.loadAll()
  }
}
</script>
