<template>
  <div>
  <div class="flex md:flex-row xs:flex-col">
    <input class="flex border-2 border-sunglow bg-rgray rounded-xl item-dark p-1 m-1" placeholder="было" v-model="beforeEl"/>
    <input class="flex border-2 border-sunglow bg-rgray rounded-xl item-dark p-1 m-1" placeholder="сейчас" v-model="nowEl"/>
    <input class="flex border-2 border-sunglow bg-rgray rounded-xl item-dark p-1 m-1" placeholder="тариф" v-model="tarif"/>
    <span class="flex border-2 border-sunglow bg-rgray rounded-xl item-dark p-1 m-1">{{"= " + Summ() + " руб."}}</span>
  </div>
  </div>
</template>
<script>
export default {
  name: "list",
  data() {
    return {
      baseT: "введите текст",
      tarif: 5.73,
      beforeEl: "",
      nowEl: ""
    }
  },
  methods: {
    sortABC(){
      return this.baseT.split('').sort().join('')
    },
    Summ(){
      return Math.round((this.nowEl - this.beforeEl) * this.tarif)
    }
  }
}
</script>