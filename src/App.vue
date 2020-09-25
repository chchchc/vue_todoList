<template>
  <div id="app">
    <input
      @keydown.enter="addTask"
      class="edit"
      type="text"
      v-model="task.content"
      placeholder="编写任务" />

      <div>待办列表</div>
      <p v-if="isEmpty" class="empty">暂无待办任务</p>
      <div class="list">
        <div class="unit" v-for="(item,index) in list" :key="item.content">
          <input
            @click="changeState(index)"
            :checked="item.finished"
            type="checkbox">
          <span :class="{'isfinish':item.finished}">{{item.content}}</span>
          <button class="del" @click="removeTask(index)">删除</button>
          <button class="done" @click="doneTask(item,index)">已完成</button>
        </div>
      </div>

      <div>已办列表</div>
      <div class="list">
        <div class="unit" v-for="(el) in doneList" :key="el.content">{{el.content}}</div>

      </div>


    <!-- <HelloWorld /> -->
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  data() {
    return {
      task: {
        content: "", //内容为空
        finished: false, //未完成
        deleted: false //未删除
      },
      list:[],
      doneList:[]
    };
  },
  components: {
    HelloWorld
  },
  computed:{
    isEmpty:function(){
      return this.list.length === 0

    }
  },
  methods:{
    //添加任务
    addTask:function(){
      //将task存入list数组
      console.log('hh',this.task)
      this.list.push(this.task);
      //存入list后，重置task
      this.task = {
        content:'',
        finished:false,
        deleted:false
      }
    },
    changeState:function(index){
      let curState = this.list[index].finished;
      this.list[index].finished = !curState;
      console.log('jijiji',this.list[index].finished)
    },
    removeTask:function(index){
      //使用splice操作删除数组指定项
      this.list.splice(index,1);
    },
    doneTask:function(item,index){
      //把数组加入到已完成项中
      console.log('index',index)
      console.log('item',item)
      this.list.splice(index,1)
      this.doneList.push(item)
    }
  }
};
</script>

<style>

.edit{
  display: block;
  width: 80%;
  height: 35px;
  line-height: 35px;
  margin: 30px auto;
  box-sizing: border-box;
  padding-left:4px ;
  border-radius: 4px;
  border: 1px solid #ccc;
  outline: 0;
  box-shadow: 0 0 5px #ccc;
}
.list{
  margin: 0 auto;
  width: 80%;
}
.unit{
  position: relative;
  padding: 10px 0;
  border-bottom: 1px solid #efefef;
}
.unit:last-child{
  border-bottom: 0;
}
.isfinish{
  text-decoration: line-through;
  color: #ccc;
}
.del{
  background: red;
  text-decoration: none;
  position: absolute;
  right: 55px;
  font-size: 12px;
  border: 0;
  outline: 0;
  padding:2px 5px;
  border-radius: 5px;
  color:#fff;
}
.done{
  background: rgb(103, 187, 103);
  text-decoration:none ;
  position: absolute;
  right: 0;
  font-size: 12px;
  border: 0;
  outline: 0;
  padding: 2px 5px;
  border-radius: 5px;
  color: #fff;
}
.empty{
  font-size: 13px;
  color: #ccc;
  text-align: center;
  padding: 10px 0;
}

</style>
