<template>
<div id="list-rendering">
  <ol class="grid grid-cols-1 gap-1 my-5">
    <transition-group name="list">
    <li class="list-item"
    v-for="item in todos"
    v-bind:key="item.id"
    >
    <div class="flex border-2 border-sunglow bg-rgray rounded-xl item-dark p-1">
    <input placeholder="Новая запись" class="p-2" v-model="item.title" @input="saveTodos()"/>
    <button @click="delElem(item)"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="#64bf0a" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><line x1="15" y1="9" x2="9" y2="15"></line><line x1="9" y1="9" x2="15" y2="15"></line></svg></button>
    </div>
    </li>
    </transition-group>
  </ol>
  <div class="flex justify-center items-center">
  <button class="border-2 rounded-md border-sunglow bg-rgray p-1 mr-2 w-full" @click="addElem()">Добавить</button>
  <button class="border-2 rounded-md border-sunglow bg-rgray p-1 w-full" @click="clearTodos()">Очистить все</button>
  </div>
</div>
</template>

<script>
export default {
  name: 'test',
  data() {
    return {
      todos: [],
    }
  },
  components: {
  },
  computed:{
  },
  methods: {
    addElem(){
      this.todos.push({id: this.idGen(), title: ''});
      this.saveTodos();
    },
    delElem(item){
      this.todos.splice(this.todos.indexOf(item), 1);
      this.saveTodos();
    },
    saveTodos() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem('todos',parsed);
    },
    clearTodos() {
      this.todos.splice(''),
      localStorage.removeItem('todos');
    },
    idGen() {
      return '_' + Math.random().toString(36).substr(2, 9);
    }
  },
  mounted() {
    if (localStorage.getItem('todos')) {
      try {
        this.todos = JSON.parse(localStorage.getItem('todos'));
      }
      catch(e) {
        localStorage.removeItem('todos');
      }
    }
  },
  watch: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.list-item {
  @apply my-2 items-center justify-center;
  display: flex;
  margin-right: 10px;
}
.list-enter-active, .list-leave-to {
  transition: all 0.5s;
}
.list-enter /* .list-leave-active до версии 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
.list-leave-to {
  transform: translateX(-400px);
  opacity: 0;
}
</style>
