<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
    </div> -->
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
<script>
  export default {
    watch: {
      //監聽值
    },
    computed: {
      //相依的資料改變時才做計算方法
    },
    methods: {
      // 初始
    },
    //BEGIN--生命週期
    beforeCreate: function() {
      //實體初始化
    },
    created: function() {
      //實體建立完成。資料 $data 已可取得，但 $el 屬性還未被建立。
      this.src = this.$options.__file ;
    },
    beforeMount: function() {
      //執行元素掛載之前。
    },
    mounted: function() {
      //元素已掛載， $el 被建立。
    },
    beforeUpdate: function() {
      //當資料變化時被呼叫，還不會描繪 View。
    },
    updated: function() {
      //當資料變化時被呼叫，還不會描繪 View。
    },
    beforeDestroy: function() {
      //實體還可使用。
    },
    destroyed: function() {
      //實體銷毀。
    }
    //END--生命週期
  }
  </script>