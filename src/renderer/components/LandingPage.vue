<template>
  <div class="outside-border">
  <!--  <el-menu mode="horizontal" class="header">
        <el-menu-item index="1" @click="clickSave">保存</el-menu-item>
        <el-menu-item index="2" @click="SaveAnotherPlace">导出</el-menu-item>
       <el-submenu index="1">
       <template slot="title">文件(F)</template>
        <el-menu-item index="1-1">新建</el-menu-item>
        <el-menu-item index="1-2">打开</el-menu-item> 
        <el-menu-item index="1-3" @click="clickSave">保存</el-menu-item>
        <el-menu-item index="1-4" @click="SaveAnotherPlace">另存为</el-menu-item>
        <el-menu-item index="1-5">退出</el-menu-item>
      </el-submenu>
      <el-submenu index="2">
        <template slot="title">编辑(E)</template>
        <el-menu-item index="2-1">撤销</el-menu-item>
        <el-menu-item index="2-2">剪切</el-menu-item>
        <el-menu-item index="2-3">复制</el-menu-item>
        <el-menu-item index="2-4">粘贴</el-menu-item>
        <el-menu-item index="2-5">删除</el-menu-item>
      </el-submenu>
       <el-submenu index="3">
        <template slot="title">格式(O)</template>
        <el-menu-item index="3-1">自动换行</el-menu-item>
        <el-menu-item index="3-2">字体</el-menu-item>
      </el-submenu>
       <el-submenu index="4">
        <template slot="title">查看(V)</template>
        <el-submenu index="4-1">
          <template slot="title">缩放</template>
          <el-menu-item index="4-1-1">放大</el-menu-item>
          <el-menu-item index="4-1-2">缩小</el-menu-item>
          <el-menu-item index="4-1-3">恢复默认缩放</el-menu-item>
        </el-submenu>
        <el-menu-item index="4-2">状态栏</el-menu-item>
      </el-submenu>
       <el-submenu index="5">
        <template slot="title">帮助(H)</template>
        <el-menu-item index="5-1">查看帮助</el-menu-item>
        <el-menu-item index="5-2">关于记事本</el-menu-item>
      </el-submenu>
  
    </el-menu>
    
      <el-input v-model="input" type="textarea" autosize placeholder="随笔记录"></el-input>
    -->
    <h6 class="header">记事本</h6>
     <div class="main">
      <input type="text" v-model="input" @keyup.enter="add" class="context" placeholder="随笔记录"/>
      <ul>
        <li v-for="(data, index) in datalist" :key="index" class="listyle">
          <hr class="hrstyle" />
          <span>{{ index + 1 }}.{{ data }}</span>
          <span>
            <button class="deletebtn" @click="deletebtn(index)">
              <i class="el-icon-close"></i>
            </button>
          </span>
        </li>
      </ul>
    </div>
    <footer class="footer">
      <hr />
      <a>It has {{ datalist.length }} items now!</a>
      <span>
          <button class="clearcontext" @click="clearcontext">Delete all</button>
        </span>
    </footer>
  </div>
</template>
<script>
export default {
  data(){
    return{
      input:'',
      datalist:["吃饭"],
    }
  },
  created(){

  },
  methods:{
  /*  clickSave(){
      sessionStorage.setItem("savecontent",JSON.stringify(this.input));
      console.log(JSON.parse(sessionStorage.getItem("savecontent")));//将输入内容打印到控制台上
    },
    SaveAnotherPlace(){

    }
  */
   add() {
      this.datalist.push(this.input);
    },
    deletebtn(index) {
      this.datalist.splice(index, 1);
    },
    clearcontext() {
      this.datalist = [];
    },
  },
}
</script>
<style lang="scss" scoped>
.outside-border {
 // border: 1px solid rgb(194, 188, 188);
//  box-shadow: 0 0 9px 3px #999;
  min-width: 100%;
  max-width: 100%;
  color: #4d4d4d;
  font: 14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
  background: #fff;
}

.header {
  left: center;
  width: 100px;
  margin: 0 auto;
  font-size: 30px;
  text-shadow: 3px 5px 5px #656b79;
}

.main {
  left: center;
  width: 100%;
  margin: 0 auto;
}

.context {
  width: 99.5%;
  font: 14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 20px;
  color: #4d4d4d;
  border-width: 0;
  height: 40px;
  background: #ffffff;
  outline: none;
}

ul {
  margin: 0;
  padding: 0;
  text-align: left;

  .listyle {
    list-style-type: none;
    font-size: 18px;
  }
}

.deletebtn {
  border-width: 0;
  background: #ffffff;
  float: right;
  outline: none;
  cursor: pointer;
}

.footer {
  float: bottom;
}

.hrstyle {
  border: solid 1px #e5e5e5;
}

.clearcontext {
  border-width: 0;
  background: #ffffff;
  float: right;
  outline: none;
  cursor: pointer;
  font-size: 12px;
  font: 12px 'Helvetica Neue', Helvetica, Arial, sans-serif;
}
</style>