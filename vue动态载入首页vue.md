


## Vue加载组件的几种方式，具体代码如下所示：

//正常加载
import index from '../pages/index.vue'
import view from '../pages/view.vue'
//懒加载
const index = resolve => require(['../pages/index.vue'], resolve)
const view = resolve => require(['../pages/view.vue'], resolve)
//懒加载 - 按组
const index = r => require.ensure([], () => r(require('../pages/index.vue')), 'group-index')
const view = r => require.ensure([], () => r(require('../pages/view.vue')), 'group-view')
// 懒加载 - 按组 import，基于ES6 import的特性
const index = () => import('../pages/index.vue')
const view = () => import('../pages/view.vue')


动态加载组件的四种方式：

## 1、使用import导入组件，可以获取到组件

var name = 'system';
var myComponent =() => import('../components/' + name + '.vue');
var route={
  name:name,
  component:myComponent
}
## 2、使用import导入组件，直接将组件赋值给componet

var name = 'system';
var route={
  name:name,
  component :() => import('../components/' + name + '.vue');
}
## 3、使用require 导入组件，可以获取到组件

var name = 'system';
var myComponent = resolve => require.ensure([], () => resolve(require('../components/' + name + '.vue')));
var route={
  name:name,
  component:myComponent
}
## 4、使用require 导入组件，直接将组件赋值给componet

var name = 'system';
var route={
  name:name,
  component(resolve) {
    require(['../components/' + name + '.vue'], resolve)
  }
}