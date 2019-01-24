<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper' ]">
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim';
import SearchInput from '@/components/SearchInput';
import HeroImage from '@/components/HeroImage';
import Item from '@/components/Item';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
  },
  data() {
    return{
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .wrapper{
    display:flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color:white;
    margin: 0;
    padding:30px;
    min-height: 100vh;

    &.flexStart {
      justify-content: flex-start;
    }
  }
</style>
