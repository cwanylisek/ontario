<template lang="html">
  <div id="app">
    <button class="btn" v-on:click="fetchData">test fetch</button>
    <br>
    <br>
    <br>
    <div class="tabdata">
      <!-- <div>
        {{tables.features[6].properties.Fax}}

      </div> -->

      <div>
        <table class="tabdata">
          <tr>
            <th>Fax</th>
            <th>Kod Pocztowy</th>
            <th>Miasto</th>
            <th>Nazwa</th>
            <th>Kierunkowy</th>
            <th>Telefon</th>
            <th>Ulica</th>
            <th>Wojewodztwo</th>
          </tr>
          <!-- schemat handlingu dla zagnieżdżonych danych z json -->
          <tr v-for="feature in tables.features">
            <td>{{feature.properties.Fax}}</td>
            <td>{{feature.properties.Kod_pocztowy}}</td>
            <td>{{feature.properties.Miasto}}</td>
            <td>{{feature.properties.Nazwa}}</td>
            <td>{{feature.properties.Nr_kierunkowy}}</td>
            <td>{{feature.properties.Telefon}}</td>
            <td>{{feature.properties.Ulica}}</td>
            <td>{{feature.properties.Wojewodztwo}}</td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: 'app',
  data() {
    return {
      tables: [{
        features: [{
          geometry: [],
          properties: {}
        }]
      }],
      msg: 'elo ziomek'
    }
  },
  methods: {
    fetchData() {
      fetch(`https://divi.io/api/features/Mjk4.zHivJ8D_UnN8enwd1pNAKrBwUCg`, {
        method: 'GET'
      }).then(response => response.json())
        .then(json => console.log(json))
    },
    fetchApi() {
      fetch(`https://divi.io/api/features/Mjk4.zHivJ8D_UnN8enwd1pNAKrBwUCg`, {
        method: 'GET'
      }).then(response => response.json())
        .then(json => this.tables = json)
    },
    selectAll() {
      var i = 0
      for (i = 0; i < 100; i++);
    }
  },
  created() {
    this.fetchApi()
  }
}

</script>

<style lang="css">
</style>
