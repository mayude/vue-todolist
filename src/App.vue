<template>
  <div>
    <div class="page-group">
      <div class="page page-current" id="main">
        <AppHeader></AppHeader>
        <div class="content">
          <div class="content-block">
            <div v-for="(item, index) in list" :key="index">
              <Item :items="list" :item="item" :index="index"></Item>
            </div>
          </div>
        </div>
      </div>
  
      <div class="page" id="edit">
        <Edit :items="list"></Edit>
      </div>
    </div>
  </div>
</template>

<script>
import AppHeader from './components/appHeader.vue'
import Item from './components/item.vue'
import Edit from './components/edit.vue'

export default {
  name: 'app',
  data() {
    return {
      list: []
    }
  },
  components: {
    AppHeader,
    Item,
    Edit
  },
  mounted: function () {
    this.$http.get('./data/data.json').then((res) => {
      this.list = res.data;
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
