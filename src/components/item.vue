<template>
  <div class="card" v-bind:class="{done: isDone}">
    <div class="card-header">
      <span class="card-title">{{item.title}}</span>
      <input name="check" type="checkbox" @click="isDone=!isDone"/>
    </div>
    <div class="card-content">
      <div class="card-content-inner">{{item.content}}</div>
    </div>
    <div class="card-footer"> 
      <span class="date">{{item.date}}</span>
      <a><span class="icon icon-remove" @click="delItem(index)"></span></a>
    </div>
  </div>
</template>

<script>
export default {
  props: ["items", "item", "index"],
  data() {
    return {
      isDone: false,
      itemList: this.items
    }
  },
  watch: {
    items(val) {
      this.itemList = val;
    },
    itemList(val) {
      this.$emit("item changed", val);
    }
  },
  methods: {
    delItem: function(index) {
      $.confirm('是否删除这条记录？', () => {
          this.itemList.splice(index, 1);
      });
    }
  }
}
</script>

<style lang="scss">
.card-content-inner {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.card-title {
  font-weight: bold;
}
.date {
  font-size: 0.5rem;
}
.done {
  color: #CCC;

  .card-title {
    text-decoration: line-through;
    text-decoration-color: #999;
    -moz-text-decoration-color: #999;
  }
}
</style>

