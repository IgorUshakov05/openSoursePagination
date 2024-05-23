<template>
    <div class="filter">
        <h2>Фильтр</h2>
        <div class="filterSerachInstrument">
            <input v-model="formData.text" @input="emitData()" type="text" class="inputName" name="text" id="firstName" placeholder="Enter Name">
    <div   class="myInputTypeRadio" :class="{
  'uncknownActive': formData.status === 'unknown',
  'deadActive': formData.status === 'dead',
  'aliveActive': formData.status === 'alive'
}">
                <div @click="setStatus('dead')" class="dead">Dead</div>
                <div @click="setStatus('unknown')" class="unknown">Unknown</div>
                <div @click="setStatus('alive')" class="alive">Alive</div>
            </div>
        </div>
    </div>
</template>


<script>
export default {
  props: ['text', 'status'],
  data() {
    return {
      formData: {
        text: "".trim(),
        status: null
      }
    }
  },
  methods: {
    setStatus(value) {
      if(this.formData.status === value) {
          this.formData.status = null
          this.$emit('changeData', this.formData);
          return false
      }
      this.formData.status = value
      this.$emit('changeData', this.formData);
    },
    emitData() {
      this.$emit('changeData', this.formData);
    },
  
  }
}
</script>