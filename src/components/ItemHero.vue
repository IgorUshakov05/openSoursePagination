<script setup>
    defineProps({
        nameHero: String,
        alive: String,
        place: String,
        lastSeen: String,
        img: String,
        species:String
})
</script>

<template>
    <li class="cardItem">
                <div class="picHero">
                    <img :src="img" alt="Photo">
                </div>
                <div class="infOfHero">
                    <div class="mainInfo">
                        <h1 class="namePers">{{nameHero}}</h1>
                        <h2 class="isLIve"><span :class="{
  'uncknownStatus': alive === 'unknown',
  'deadStatus': alive === 'Dead',
  'aliveStatus': alive === 'Alive'
}"></span>{{alive}} - {{species}}</h2>
                    </div>
                    <div class="location">
                        <p>Last known location:</p>
                        <h3>{{place}}</h3>
                    </div>
                    <div class="location">
                        <p>First seen in:</p>
                        <h3>{{lastSeen}}</h3>
                    </div>
                </div>
            </li>
</template>