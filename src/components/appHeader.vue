<template>
  <header class="bar bar-nav">
    <a class="icon icon-edit pull-right" href="#edit" @click="addItem"></a>
    <h1 class="title">todoList</h1>
  </header>
</template>

<script>
import bus from './../eventBus.js'

export default {
  methods: {
    addItem: function() {
      bus.$emit("add-item");
    }
  }
}
</script>

