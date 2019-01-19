<template>
  <div class="wrapper">
    <HeroImage/>
    <Claim/>
    <SearchInput v-model="searchValue" @input="handleInput"/>
    <ul>
      <li v-for="item in results" :key="item.data[0].nasa_id">
          <p>{{item.data[0].description}}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim';
import SearchInput from '@/components/SearchInput';
import HeroImage from '@/components/HeroImage';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    HeroImage,
  },
  data() {
    return{
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  .wrapper{
    display:flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color:white;
    margin: 0;
    padding:30px;
    min-height: 100vh;
  }
</style>
