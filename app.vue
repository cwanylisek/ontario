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
            <th @click="sort('Fax')">Fax</th>
            <th @click="sort('Kod_pocztowy')">Kod Pocztowy</th>
            <th @click="sort('Miasto')">Miasto</th>
            <th @click="sort('Nazwa')">Nazwa</th>
            <th @click="sort('Nr_kierunkowy')">Kierunkowy</th>
            <th @click="sort('Telefon')">Telefon</th>
            <th @click="sort('Ulica')">Ulica</th>
            <th @click="sort('Wojewodztwo')">Wojewodztwo</th>
          </tr>
          <!-- schemat handlingu dla zagnieżdżonych danych z json -->
          <tr v-for="feature in sortedTables">
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
      msg: 'elo ziomek',
      currentSort: 'name',  // rodzaj sortowania
      currentSortDir: 'asc'  // kierunek aktualnego sortowania
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
    sort:function(s) {
      //if s == current sort, reverse
      if(s === this.currentSort) {
        this.currentSortDir = this.currentSortDir==='asc'?'desc':'asc';
      }
      this.currentSort = s;
    }
  },
  computed: {
    sortedTables:function() {
    return this.features.sort((a,b) => {
      let modifier = 1;
      if(this.currentSortDir === 'desc') modifier = -1;
      if(a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
      if(a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
      return 0;
    });
  }
  },
  created() {
    this.fetchApi()
  },
}

</script>

<style lang="css">
</style>
