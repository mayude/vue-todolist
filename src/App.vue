<template>
  <div>
    <div class="page-group">
          <!-- 单个page ,第一个.page默认被展示-->
      <div class="page">
          <!-- 标题栏 -->
        <header class="bar bar-nav">
          <a class="icon icon-menu pull-left open-panel"></a>
          <a class="icon icon-edit pull-right"></a>
          <h1 class="title">todoList</h1>
        </header>

        <div class="content">
          <div class="content-block">
            <div v-for="(item, index) in list" :key="index">
              <Item :items="list" :item="item" :index="index"></Item>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Left Panel with Reveal effect -->
    <div class="panel panel-left panel-reveal">
      <div class="content-block">
        <p>这是一个侧栏</p>
        <p></p>
        <!-- Click on link with "close-panel" class will close panel -->
        <p><a href="#" class="close-panel">关闭</a></p>
      </div>
    </div>
  </div>
</template>

<script>
import Item from './components/item.vue'

export default {
  name: 'app',
  data () {
    return {
      list: []
    }
  },
  components: {
    Item
  },
  mounted: function() {
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
