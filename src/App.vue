<template>
  <div id="app">
    <Mylist v-bind:message="message" v-on:result-event="appAction"/>
      <hr>
      <div>
      <table v-html="log" align="center"></table>
      </div>
  </div>
</template>

<script>
import Mylist from './components/Mylist.vue'
export default {
  name: 'app',
  components: {
    Mylist
  },
  data:function(){
    return {
      message: 'メモを入力してください',
      mylist:[],
    };
  },
  computed:{
    log:function(){
      var table='<tr><th class="head">my list</th></tr>';
      for(var i in this.mylist){
        table += '<tr><td>' + this.mylist[i] + '</td></tr>';
      }
      return table;
    }
  },
  created:function(){
    var items = localStorage.getItem('log');
    var logs = JSON.parse(items);
    if(logs != null){ this.result = logs; }
  },
  methods:{
    appAction:function(textbox){
      this.mylist.unshift([textbox]);
      if(this.mylist.length>5){
        this.mylist.pop();
      }
      var log = JSON.stringify(this.mylist);
      localStorage.setItem('log', log);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
table{
  border:1px solid gray;
}
tr th.head{
  background-color:black;
  color:white;
}
</style>