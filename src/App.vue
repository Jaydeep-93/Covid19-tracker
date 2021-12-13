<template>
  <!-- Header for App -->
  <Header />

  <div class="container">
  
  <!-- Body -->
  <main class="" v-if="!loading">
    
    <DataTitle :text="title" :dataDate="dataDate"/>

    <DataBoxes :stats="stats"/>

    <CountrySelect :countries="countries" @get-country="getCountryData" />

  </main>
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching data</div>
    <img :src="loadingImage" alt="loadingImage" class="w-24 m-auto">
  </main>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import DataTitle from "./components/DataTitle.vue"
import DataBoxes from "./components/DataBoxes.vue"
import CountrySelect from "./components/CountrySelect.vue"

export default {
  name: "App",
  components: {
    Header,
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('./assets/hourglass.gif')
    }
  },
  methods: {
    async fetchCoviData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = res.json();
      return data;
    },
    getCountryData(country) {
      this.title = country.Country
      this.stats = country
    }
  },
  async created() {
    const data = await this.fetchCoviData();
    this.dataDate = data.Date  
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
    console.log(data);
  },
};
</script>

