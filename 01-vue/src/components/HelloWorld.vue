<template>
  <div class="hello">
    <!-- 子传父，emit派发 -->
    <h1 @click="$emit('foo', 'abc')">{{ msg }}</h1>

    <!-- 桥接方式 -->
    <button @click="sendMsg">给兄弟打招呼</button>
    <p>{{ foo.$options.name }}</p>

    <!-- 匿名插槽插槽 -->
    <slot></slot>

    <!-- 具名插槽 -->
    <p><slot name="content"></slot></p>

    <!-- 作用域插槽 -->
    <p><slot name="footer" foo="foo" bar="bar"></slot></p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  // 拿参：注入
  inject: ['foo'],
  mounted(){
    this.$parent.$on('foo', () => {
      // 会触发两次，因为自己派发也会监听
      console.log('兄弟传来的信息');
    })
  },
  methods: {
    sendMsg() {
      this.$parent.$emit('foo');

      // $root
      // $bus
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
