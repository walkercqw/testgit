<template>
  <div id="app">
    <div class="buttons">
      <button @click="movediv" v-show="!ismove">移动</button>
      <button @click="sureMove" v-show="ismove">确认</button>
      <button @click="notMove" v-show="ismove">取消</button>
    </div>
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
      ismove:false,
      moveList:[]
    }
  },
  methods:{
    isactive(index){
      const a = this.divList[index]
      if(this.ismove){
        if(!a.active){
            if(this.targetIndex == index){
            this.targetIndex = -1;
          } else{
            this.targetIndex = index;
          } 
        } else {
          alert("这张是要移动的")
        }           
      } else{  
        this.divList[index].active = !a.active
        let haveIt = this.hasItem(index)     
        if(a.active){
          if(!haveIt){
            this.moveList.push(a)
            console.log("数组中没有" + this.moveList)
          } 
        }else{
          if(haveIt){
            this.moveList.splice(this.moveList.indexOf(a),1)
            console.log("数组中有了" + this.moveList)
          }
        }
      }
      console.log("最终的逻辑实现"+ this.moveList)
    },
    movediv(){
      const willMove = this.divList.some((item) => {
        return item.active
      })
      if(!willMove){
        alert("请选择要移动的图片")
        return
      }
      this.ismove = !this.ismove
      if(!this.ismove) {
        this.targetIndex = -1;
      }
    },
    hasItem(index){
      let count = this.divList[index].value
      return this.moveList.some(function(item){
        console.log(item.value)
        console.log(count)
        return item.value == count
      })
    },
    sureMove(){
      const target = this.divList
      if(this.targetIndex == -1){
        alert("请选择要移动的位置")
        return
      } else {
        this.ismove = !this.ismove
        for(var i = 0; i < this.moveList.length;i++){
          const item = this.moveList[i]
          this.divList.splice(this.divList.indexOf(item),1)
        }
        if(this.divList.indexOf(target[this.target]) == 0){
          this.divList.unshift(...this.moveList)
        }else{
          this.divList.splice(this.divList.indexOf(target[this.target]),0,...this.moveList)
        }
        console.log(this.divList)
        for(var i = 0; i < this.divList.length; i++){
          this.divList[i].active = false;
          this.targetIndex = -1
        }
      }
    },
    notMove(){
      this.ismove = !this.ismove
      this.targetIndex = -1
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
.buttons{
  width:100px;
  background-color: #fff;
  overflow: hidden;
}
button{
  float:left
}
.active{
  border: 5px solid skyblue;
}
.target{
  border:5px solid gray
}
</style>
