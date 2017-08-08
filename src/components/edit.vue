<template>
  <div>
    <header class="bar bar-nav">
      <a class="button button-link button-nav pull-left" @click="quit()">
        <span class="icon icon-left"></span>
      </a>
      <a class="button button-link button-nav pull-right" @click="saveItem()">
        <span class="icon icon-check"></span>
      </a>
      <h1 class='title'>新增条目</h1>
    </header>
    <div class="content">
      <div class="list-block">
        <ul>
          <li>
            <div class="item-content">
              <div class="item-inner">
                <div class="item-title label">标题</div>
                <div class="item-input">
                  <input id="title" 
                    type="text" 
                    placeholder="不得超过12个字符"
                    v-model="itemTitle" 
                    value="itemTitle" />
                </div>
              </div>
            </div>
          </li>
          <li>
            <div class="item-content">
              <div class="item-inner">
                <div class="item-input">
                  <textarea id="content-text" v-model="itemContent"></textarea>
                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import bus from './../eventBus.js'

export default {
  props: ["items"],
  data() {
    return {
      itemList: this.items,
      itemTitle: '',
      itemContent: '',
      modifyIndex: -1
    }
  },
  mounted: function() {
    bus.$on("modify-item", (index) => {
      this.modifyIndex = index;
      this.itemTitle = this.itemList[index].title;
      this.itemContent =  this.itemList[index].content;
    });
    bus.$on("add-item", () => {
      this.modifyIndex = -1;
      this.itemTitle = "";
      this.itemContent =  "";
    });
  },
  watch: {
    items(val) {
      this.itemList = val;
    },
    itemList(val) {
      this.$emit("item changed", val);
    },
    itemTitle(val) {
      if (val.length > 12) {
        this.itemTitle = val.substring(0, 12);
      }
    }
  },
  methods: {
    getCurTime: function() {
      var myDate = new Date();
      return myDate.getFullYear() + '年' + myDate.getMonth() + '月' 
        + myDate.getDate() + '日 ' + myDate.getHours() + ':' + myDate.getMinutes();
    },
    saveItem: function() {
      if (this.itemTitle == "") {
        $.alert('请至少填写标题');
        return;
      }
      var newItem = {
        title: this.itemTitle,
        content: this.itemContent,
        date: this.getCurTime()
      }
      if (this.modifyIndex >= 0) {
        this.itemList.splice(this.modifyIndex, 1);
      }
      this.itemList.unshift(newItem);
      window.history.go(-1);
    },
    quit: function() {
      if(this.itemTitle == '' && this.itemContent == '') {
        window.history.go(-1);
        return ;
      }
      $.confirm('是否放弃编辑？', () => {
        window.history.go(-1);
      });
    }
  }
}
</script>

<style lang="scss">
.list-block {
  margin: 0;
  height: 100%;
  ul {
    height: 100%;
  }
}
</style>


