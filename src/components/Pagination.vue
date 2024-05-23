<script setup>
 defineProps({
    active: String,
    maxValue:String
})
</script>

<template>
    <div class="pagination">
           <div class="prev" @click="$emit('goPrev')">
               <svg width="14" height="22" viewBox="0 0 14 22" fill="none" xmlns="http://www.w3.org/2000/svg">
                   <path d="M12 2L3 11L12 20" stroke="white" stroke-width="3" />
                 </svg>
           </div>
           <ul class="paginationItems">
               <li>{{active===1?maxValue:active-1}}</li>
               <li class="active">{{active}}</li>
               <li>{{active===maxValue?"1":active+1}}</li>
           </ul>
           <div class="next" @click="$emit('goNext')">
               <svg width="14" height="22" viewBox="0 0 14 22" fill="none" xmlns="http://www.w3.org/2000/svg">
                   <path d="M2 20L11 11L2 2" stroke="white" stroke-width="3" />
                 </svg>
           </div>
       </div>
       <p>
       {{ activeLink }}
   
       </p>
   </template>