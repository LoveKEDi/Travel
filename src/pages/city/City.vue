<template>
<div>
  <CityHeader></CityHeader>
  <CitySearch :cities="cities"></CitySearch>
  <CityList :cities="cities" :hotCities="hotCities" :letter="letter"></CityList>
  <CityAlphabet :cities="cities" @change="handleLetterChange"></CityAlphabet>
</div>
</template>

<script>
import axios from 'axios'
import CityHeader from './components/header'
import CitySearch from './components/search'
import CityList from './components/list'
import CityAlphabet from './components/alphabet'
export default{
  name: 'City',
  components:{
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter:''
    }
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.handleCityInfoSucc)
    },
    handleCityInfoSucc (res) {
      res = res.data
      if (res.ret && res.data){
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    handleLetterChange (letter) {
      this.letter = letter
    }
  },
  mounted() {
    this.getCityInfo()
  }
}
</script>

<style lang="stylus" scoped>
</style>
