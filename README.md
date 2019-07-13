# 前端面试题收集

## Experience
- 在项目中负责什么角色？
> 

## Vue

- `v-if` 和 `v-for` 哪个优先级更高？
  - 基本回答：`v-for` 级别更高
  - 进阶回答：这两个就[不应该同时使用在同一个元素上](https://cn.vuejs.org/v2/style-guide/#%E9%81%BF%E5%85%8D-v-if-%E5%92%8C-v-for-%E7%94%A8%E5%9C%A8%E4%B8%80%E8%B5%B7-%E5%BF%85%E8%A6%81)。如果是整个列表需要判断隐藏，则应该把 `v-if` 放在父级元素上；而如果是列表内容需要过滤，则应该使用计算属性等方式，返回过滤后的列表。养成推荐的风格习惯后，平时也不必多虑哪个优先级高的问题。

- 计算属性 `computed` 和侦听器 `watch` 有什么区别？
  - 基本回答：计算属性有缓存。
  - 进阶回答：
    - 计算属性只在相关响应式依赖发生改变时它们才会重新求值。它的使用场景本来是，将 `template` 中复杂的计算逻辑提取出来，一来是结构和行为分离的原则；二来是方便重用。
    - `watch` 常用于观察和响应 Vue 实例上的数据变动。当需要在数据变化时，执行异步或开销较大的操作时使用更合适。
    - `watch` 支持初始化监听以及对象深监听。
    - `watch` 支持取消监听。
    - `watch` 要注意不要滥用。要获取多个独立属性关联的结果，应该用计算属性代替。
  - 追问一：`watch` 如何监听对象？能否监听对象的变更？
    - 需要设置属性：`deep: true`，并且被监听对象是“能被 Vue 的响应式系统追踪的状态”，即在初始化时已定义好对象的结构，或在后期通过 `$set` 进行响应式设值。特别地，如果是“数组对象”，则数组元素的增删操作，能被直接监听，而无须设置此属性。
  - 追问二：计算属性能否做到同样的操作，如果用计算属性的话怎么做？哪个好？

- `mixin` 和 `mixins` 的区别？？？
  - 基本回答：
  - 进阶回答：……不应滥用。

- 在 Vue 中，如何强制刷新组件？
  - 基本回答：`$forceUpdate`。
  - 进阶回答：……但这个方法应该避免使用，而优先检查各种更新依赖的可靠性，以避免潜在的 BUG。

- 生命周期钩子 `beforeDestroy` 何时使用
  - 基本回答：Vue 实例销毁之前调用。
  - 进阶回答：
    - 区别于 `destroyed`，在 `beforeDestroy` 这一周期中，Vue 实例仍然完全可用。
    - 该钩子在服务器端渲染期间不被调用。