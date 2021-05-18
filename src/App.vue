<template>
  <div id="app">
    <div>
      <p>please enter array blow, separating each element with comma, and then click the button</p>
      <p>example: 4,5,1,6,10</p>
      <p>when you enter a non-integer, I 'll convert it to an integer</p>
      <div class="input-box">
        <el-input v-model="arrStr" placeholder="请输入内容"></el-input>
        <el-button @click="clickButton">点击</el-button>
        <div class="result-box">
          输入的数组是{{this.cur_arr}}
          <span v-if="balance !==- 1">
            平衡点为{{this.cur_arr[balance]}}
          </span>
          <span v-else>
            当前数组没有平衡点
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// 1,2,3,0,6
export default {
  name: 'app',
  data(){
    return {
      arrStr: '',
      balance: -1,
      cur_arr: []
    }
  },
  methods:{
    clickButton(){
      let arr = this.dealArr();
      this.balance = this.balancePosition(arr);
    },
    dealArr(){
      let arr = this.arrStr.split(',');
      arr = arr.map(item => {
        if(item!=='')
          return Math.floor(Number(item));
      })
      return arr.filter(item => Number.isInteger(item));
    },
    balancePosition(arr){
      this.cur_arr = arr;
      if(arr.length <= 2){
        return -1;
      }
      for(let i = 1; i < arr.length; i++) {
        let left = 0;
        let right = 0;
        for(let j = 0; j < i; j++){
          left += arr[j]
        }
        for(let j = i + 1; j < arr.length; j++){
          right += arr[j]
        }
        if(left === right){
          return i;
        }
      }
      return -1;
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
.input-box {
  width: 50%;
  margin: 0 auto;
}
.input-box .el-button{
  margin-top: 20px;
}
.result-box {
  margin-top: 40px;
}
</style>
