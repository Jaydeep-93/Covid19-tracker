<template>
  <!-- Header for App -->
  <Header />

  <!-- Body -->
  <main class="" v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate"/>
  </main>
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching data</div>
    <img :src="loadingImage" alt="loadingImage" class="w-24 m-auto">
  </main>
</template>

<script>
import Header from "./components/Header.vue";
import DataTitle from "./components/DataTitle.vue"

export default {
  name: "App",
  components: {
    Header,
    DataTitle
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
  },
  async created() {
    const data = await this.fetchCoviData();
    this.dataDate = data.Date  
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false

  },
};
</script>

