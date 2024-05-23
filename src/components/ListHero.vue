<script setup>
    import ItemHero from './ItemHero.vue'
    defineProps({
  list: Object,
})
</script>
<template>
  <div class="cards">
        <ul class="cardsList">
           <ItemHero v-for="hero in list" v-if="list" 
           :nameHero="hero.name" 
           :img="hero.image"
            :lastSeen="hero.origin.name"
            :place="hero.location.name"
            :alive="hero.status"
            :species="hero.species" 
            :key="hero.id"/> 
        </ul>
    </div>
    
</template>
