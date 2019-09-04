<template>
  <div id="app">
    <!-- 传属性，ref -->
    <!-- @foo 对应的派发名称，注：事件派发是自己在监听，并非是父在监听 -->
    <HelloWorld
      @foo="onFoo"
      ref="hw"
      msg="Welcome to a Your Vue.js App"
    />

    <!-- 兄弟节点 -->
    <HelloWorld>
      <!-- 通常插槽会用 template 标签包裹起来 -->
      <!-- 匿名插槽 -->
      <template>abc</template>

      <!-- 具名插槽：v-slot：指定插槽的名称 -->
      <template v-slot:content>domesy</template>

      <!-- 作用域插槽：字传给父 -->
      <template v-slot:footer="slotProps">
        {{slotProps.foo}} - {{slotProps.bar}}
      </template>
    </HelloWorld>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'app',
  provide() {
    return {
      // 这个值可以在任何后代中都可以取到
      'foo': this
    }
  },
  components: {
    HelloWorld
  },
  mounted() {
    // 获取属性值
    // 通过refs
    console.log(this.$refs.hw.msg);

    // 通过$children方式，$children 是无序的，并非是有顺序的
    console.log(this.$children[0].msg);
  },
  methods: {
    onFoo(msg) {
      console.log(msg);
    }
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
