<template>
  <div class="yr">
    <p>GET - https://www.yr.no/sted/Norge/Vestfold_og_Telemark/Larvik/Tj%C3%B8lling_m%C3%A5lestasjon/varsel.xml</p>
    <p>GET - http://www.geoplugin.net/xml.gp?base_currency=EUR</p>
    <input type="text" v-model="url">
    <button @click="getData">GET</button>
    <p></p>
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  name: 'HelloWorld',
  data () {
    return {
      savedData: null,
      url: 'http://www.geoplugin.net/xml.gp?base_currency=EUR'
    }
  },
  methods: {
    getData () {
      var convert = require('xml-js')
      Vue.axios.get(this.url)
        .then((response) => {
          var result1 = convert.xml2json(response.data, {compact: true, spaces: 4})
          // var result2 = convert.xml2json(response.data, {compact: false, spaces: 4})
          this.savedData = JSON.parse(result1)
          console.log(this.savedData)
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
