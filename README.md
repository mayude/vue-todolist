# todolist
 
vue入门刚几天，这是第一个webapp。     
vue上手确实比较快，文档真的超级友好！赞！b(￣▽￣)d      
预览效果可以戳：[todoList](https://aqingc.github.io/vue-todolist/)     
     
**预览图**     
![image](https://github.com/AQingC/vue-todolist/blob/gh-pages/preview/todolist-1.png)
![image](https://github.com/AQingC/vue-todolist/blob/gh-pages/preview/todolist-2.png)

   
## 分析&总结

### 分析
> 脚手架：vue-cli          
> 技术栈：webpack + vue + vue-resource + SUI-Mobile   
   
使用的是simple-webpack模板，文件目录如下：   
    
├─.babelrc		// babel配置文件   
├─.gitignore	   
├─index.html		// 主页   
├─package.json		// 项目配置文件   
├─README.md    
├─webpack.config.js	// webpack配置文件   
├─dist			// 发布目录   
│   ├─.gitkeep        
├─src			// 开发目录	  
│   ├─App.vue		// App.vue组件   
│   ├─main.js		// 预编译入口     
       
构建完成后比vue-browserify-simple项目模板依赖要完整很多。和browserify不同的是，执行npm run dev命令后并不会在dist目录下生成build.js文件，开发环境下build.js是在运行内存中的。    

这次UI库使用的是阿里写的SUI-Moblie，当时是看到风格就果断使用了，实际用上感觉不太好。去SUI-Mobile的GitHub上一看一年前就停止更新了。。。嗯。。。应该不会再用了。
      
### 总结
这次编写主要遇到的问题主要是组件间的通信。      
第一个问题是vue2.0为了保证数据流的清晰干净取消了父子间数据的双向绑定，只能通过props由父到子进行传递。so解决办法就是使用2.0的[$emit](https://cn.vuejs.org/v2/guide/migration.html#dispatch-和-broadcast-替换)来分发事件。         
第二个问题是同级组件间的数据通信。参考网上的解决办法是创建一个中央事件总线，两个组件中引入这个事件总线，传递数据的一方用[$emit](https://cn.vuejs.org/v2/guide/migration.html#dispatch-和-broadcast-替换)来分发事件，接受数据的一方用[$on](https://cn.vuejs.org/v2/api/#vm-on-event-callback)来接收事件。不过中央事件总线来管理组件通信的方法只适用于通信需求简单一点的项目，对于更复杂的情况，Vue也有提供更复杂的状态管理模式Vuex来进行处理。

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```
