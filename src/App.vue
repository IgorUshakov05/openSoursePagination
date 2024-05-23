<script setup>
import Landing from './components/Landing.vue'
import Filter from './components/Filter.vue'
import ListHero from './components/ListHero.vue'
import Pagination from './components/Pagination.vue'

</script>

<script>
export default {
  data() {
    return {
      hero: "",
      pagination: {
        currentPage: 1,
        maxPage: 42
     },
     filterData: {
      text: null,
      status: null
     },
     filterResults: null
    }
  },
  mounted() {
    this.getPers();
  },
  methods: {
    getPers() {
      fetch(`https://rickandmortyapi.com/api/character?page=${this.pagination.currentPage}`, {
        method: "GET"
      })
      .then((res) => res.json())
      .then((res) => {
        if (res.results) {
          this.hero = res.results;
          this.pagination.maxPage = res.info.pages;
        }
      })
      .catch((e) => {
        console.log(e)
      });
    },
    goNextEvent() {
      this.filterData.text = null
      this.filterData.status  = null
      this.pagination.currentPage = this.pagination.currentPage+1===43?this.pagination.currentPage=1:this.pagination.currentPage+1
      fetch(`https://rickandmortyapi.com/api/character?page=${this.pagination.currentPage}`, {
        method: "GET"
      })
      .then((res) => res.json())
      .then((res) => {
        if (res.results) {
          this.hero = res.results;
          this.pagination.maxPage = res.info.pages;
        }
      })
      .catch((e) => {
        console.log(e)
      });
    },

    goPrevEvent() {
      this.filterData.text = null
      this.filterData.status  = 'null'
      this.pagination.currentPage = this.pagination.currentPage-1===0?this.pagination.currentPage=42:this.pagination.currentPage-1
      fetch(`https://rickandmortyapi.com/api/character?page=${this.pagination.currentPage}`, {
        method: "GET"
      })
      .then((res) => res.json())
      .then((res) => {
        if (res.results) {
          this.hero = res.results;
          this.pagination.maxPage = res.info.pages;
        }
      })
      .catch((e) => {
        console.log(e)
      });
    },
    mutation(data) {
  this.filterData.text = data.text;
  this.filterData.status = data.status;
  this.filterResults = this.hero.filter((dataItem) => {
    // Проверяем, есть ли у объекта свойства 'status' и 'name'
    if (!dataItem.status || !dataItem.name) {
      return false;
    }
    
    // Теперь проверяем условия фильтрации
    if (data.text && data.status) {
      return (dataItem.status).toLowerCase() === (data.status).toLowerCase() && (dataItem.name).includes((data.text));
    }
    if (data.status) {
      return (dataItem.status).toLowerCase() === (data.status).toLowerCase();
    }
    if (data.text) {
      return ((dataItem.name).toLowerCase()).includes((data.text).toLowerCase());
    }
    // Если ни одно из условий не выполнено, возвращаем false
    return false;
  });
}}
  }
</script>

<template>
   <Landing />
   <Filter ref="filterComponent" @changeData="mutation" :text="filterData.text" :status="filterData.status"/>
   <ListHero :list="hero" v-if="!filterData.text && !filterData.status"></ListHero>
<ListHero :list="filterResults" v-else-if="filterResults.length !== 0"></ListHero>
<h1 class="notFound" v-else>Ничего не найдено</h1>
   <Pagination  @goNext="goNextEvent" @goPrev="goPrevEvent" :maxValue="pagination.maxPage" :active="pagination.currentPage" />
  </template>
  

  
  <style scoped>
  </style>