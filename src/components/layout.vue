<template>
<div class="wrapper">
  <div class="wrapper-page" :class="selected">
  <div id="app" class="container">
    <select class="text-black bg-white" v-model="selected" @change="saveTheme()">
      <option v-for="theme in themes" :key="theme.value" :value="theme.value">{{theme.text}}</option>
    </select>
    <div class="flex items-center justify-center">
      <svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" viewBox="0 0 24 24" fill="none" stroke="#64bf0a" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
    <path d="M20 9v11a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V9"/>
    <path d="M9 22V12h6v10M2 10.6L12 2l10 8.6"/>
    </svg>
    </div>
    <slot/>
  </div>
  </div>
</div>
</template>

<script>

export default {
  name: 'theme',
  data() {
    return {
    isList:false,
    selected:"light",
    themes:[
      {text:"Светлая", value: "light"},
      {text:"Темная", value: "dark"},
    ]
    }
  },
  components: {
  },
  methods: {
    saveTheme() {
      const parsedTheme = JSON.stringify(this.selected);
      localStorage.setItem('theme',parsedTheme);
    }
  },
  mounted() {
    if (localStorage.getItem('theme')) {
      try {
        this.selected = JSON.parse(localStorage.getItem('theme'));
      }
      catch(e) {
        localStorage.removeItem('theme');
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.light {
  background:white;
  color:black;
}
.dark {
  background: #333644;
  color:white !important;
}
.dark .item-dark {
  @apply border-darkorange bg-darkblack;
}
.dark input {
  @apply text-white;
}
.dark span {
  @apply text-white;
}
.dark svg {
  stroke: #FF9526;
}
.dark button{
  @apply border-darkorange bg-darkblack text-white;
}
.dark select {
  @apply text-white;
  background: transparent;
}
.dark #nav a.router-link-exact-active{
  @apply text-darkorange;
}
.dark #nav,.dark #nav a{
  @apply text-white;
}
</style>
