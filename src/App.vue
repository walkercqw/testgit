<template>
  <div id="app">
    <button @click="movediv">{{move.value}}</button>
    <div v-for="(item,index) in divList" :key="index" :class="[{'active':item.active},{'target':index == targetIndex}]" @click="isactive(index)">{{item.value}}</div>
  </div>
</template>

<script>

export default {
  name: 'app',
  components: {
    
  },
  data(){
    return {
      divList:[
        {value:1,active:false},
        {value:2,active:false},
        {value:3,active:false},
        {value:4,active:false},
        {value:5,active:false},
      ],
      targetIndex:-1,
      move:{
        ismove:false,
        value:"移动"
      },
      moveList:[]
    }
  },
  methods:{
    isactive(index){
      if(this.move.ismove){
        this.targetIndex = index;
      } else{
        var a = this.divList[index]
        this.divList[index].active = !a.active
        if(a.active){
          console.log(this.hasItem(index))
          if(this.hasItem(index)){
            console.log("移动队列中的"+item.value)
            return;
          } else {
            this.moveList.push(this.divList[index])
          }
        }
      }
      
    },
    movediv(){
      this.move.ismove = !this.move.ismove
      this.move.value = this.move.ismove?"取消":"移动";
      if(!this.move.ismove) {
        this.targetIndex = -1;
      }
    },
    hasItem(index){
      this.moveList.some((item) => {
            return item.value == this.divList[index].value
          })
    }
  }
}
</script>

<style lang="less" scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
div{
  box-sizing:border-box;
  text-align: center;
  line-height: 30px;
  width: 30px;
  height: 30px;
  background-color: red;
  color:#fff;
  margin-top:20px;
  cursor: default;
}
.active{
  border: 5px solid skyblue;
}
.target{
  border:5px solid gray
}
</style>
