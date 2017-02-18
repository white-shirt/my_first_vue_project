<template>
  <div class="hello">
    <h1>{{ title }}</h1>
    <input v-model="newItem" v-on:keyup.enter="addNew()">
    <div v-for="item in items">
      <input type="checkbox" class="checkboxstyle">
      <label v-on:click="toggleFinish(item)" v-bind:class="[{finished:item.isFinished},'liststyle']">{{ item.label }}</label>
    </div>
  </div>
</template>


<script>
import Store from 'src/store'
export default {
  name: 'hello',
  data: function () {
    return {
      title:'Todo List',
      items:Store.fetch(),
      newItem: ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep:true
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      });
      this.newItem = ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
  font-family: 微软雅黑,sans-serif;
}

.finished{
  text-decoration: line-through;
}

.liststyle{
  display: inline-block;
  cursor: pointer;
  margin-top: 20px;
}

.checkboxstyle{
  cursor: pointer;
}
</style>
