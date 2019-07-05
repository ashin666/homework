<template>
  <div id="app">
    <div id="nav">
      <div v-cloak>{{msg}}</div>
      <div v-text="msg"></div>
      <div v-html="msg1"></div>
      <div v-bind:title="title">我这里是title</div>
      <div v-model="model">{{model}}</div>
      <input type="text" style="width: 100%" v-model="model">
      <input type="button" value="点击我" @click="clickme">
      <div @click="pleaseclickme" style="background-color: red;width: 100px;height: 100px;"></div>
      <child ref="iamchild"></child>
      <h1>跑马灯</h1>
      <button @click="run">跑起来</button>
      <button @click="stop">停下来</button>
      <h1>{{paomadeng}}</h1>
      <h2>计算器</h2>
      <input v-model="n1" type="text">
      <select v-model="symbol">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">*</option>
        <option value="/">/</option>
      </select>
      <input v-model="n2" type="text">
      <input type="button" value="=" @click="sum">
      <input v-model="result" type="text">
      <h1>v-for 和 v-key</h1>
      <div v-for="(item,index) in list">
        {{item.name}}{{item.id}}index:{{index}}
      </div>
      <h1>v-if和v-show</h1>
   <div v-if="false">我是vif</div>    <!-- 直接不加载这个模块-->
      <div v-show="false">我是v-show</div> <!--dispaly直接none-->

    </div>
    <router-view/>
  </div>
</template>
<script>
  import child from "./components/child"
  export default {
      name:"parents",
      components:{
          child
      },
      data:function(){
         return{
             msg:'大家好我是msg',
             msg1:"<h1>我是h1</h1>",
             title:'你现在看到我了嘻嘻',
             model:'hhhhhhhhhhhh',
             paomadeng:'跑起来····浪起来',
             interval:null,
             symbol:"+",
             n1:0,
             n2:0,
             result:0,
             list:[
                 {id:1,name:'zss'},
                 {id:2,name:'sdf'},
                 {id:3,name:'ihu'}
             ]
         }
      },
      methods: {
          pleaseclickme:function () {
              this.$refs.iamchild.childclick("在父组件使用")
          },
          clickme:function () {
              alert("哈哈哈哈哈哈哈哈哈哈哈")
          },
          run:function () {
              if (this.interval != null) return;
              this.interval = setInterval(()=>{
                  var start = this.paomadeng.substring(0,1)
                  var end = this.paomadeng.substring(1)
                  this.paomadeng = end + start
              },300)

          },
          stop:function () {
              clearInterval(this.interval)
              this.interval = null;
          },
          sum:function () {
              switch (this.symbol) {
                  case '+':
                      this.result =parseInt(this.n1)  + parseInt(this.n2)
                      break;
                  case '-':
                      this.result =parseInt(this.n1)  - parseInt(this.n2)
                      break;
                  case '*':
                      this.result =parseInt(this.n1)  * parseInt(this.n2)
                      break;
                  case '/':
                      this.result =parseInt(this.n1)  / parseInt(this.n2)
                      break;

              }
          }
      }
  }
</script>
<style lang="scss">
  [v-cloak]{
    display: none;
  }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
