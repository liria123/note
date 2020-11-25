<template>
  <div class="outside-border">
    <!--菜单栏-->
    <el-menu mode="horizontal" class="header">
      <el-submenu index="1">
        <template slot="title">文件(F)</template>
        <el-menu-item index="1-1" @click="clickNewNote">新建</el-menu-item>
        <el-menu-item index="1-2" @click="clickOpen">打开</el-menu-item>
        <el-menu-item index="1-3" @click="clickSave">保存</el-menu-item>
        <el-menu-item index="1-4" @click="SaveAnotherPlace">另存为</el-menu-item>
        <el-menu-item index="1-5" @click="clickExit">退出</el-menu-item>
      </el-submenu>
      <el-submenu index="2">
        <template slot="title">编辑(E)</template>
        <el-menu-item index="2-1" @click="clickBack">撤销</el-menu-item>
        <el-menu-item index="2-2" @click="clickCut">剪切</el-menu-item>
        <el-menu-item index="2-3" @click="clickCopy">复制</el-menu-item>
        <el-menu-item index="2-4" @click="clickPaste">粘贴</el-menu-item>
        <el-menu-item index="2-5" @click="clickDelete">删除</el-menu-item>
      </el-submenu>
      <el-submenu index="3">
        <template slot="title">格式(O)</template>
        <el-menu-item index="3-1"><i class="el-icon-check"></i><span>自动换行</span></el-menu-item>
        <el-menu-item index="3-2"  @click="inputStyleChange=!inputStyleChange">改变字体颜色</el-menu-item>
      </el-submenu>
      <el-submenu index="4">
        <template slot="title">查看(V)</template>
        <el-submenu index="4-1">
          <template slot="title">缩放</template>
          <el-menu-item index="4-1-1" @click="makeBig">放大</el-menu-item>
          <el-menu-item index="4-1-2" @click="makeSmall">缩小</el-menu-item>
          <el-menu-item index="4-1-3" @click="makeDefault">恢复默认缩放</el-menu-item>
        </el-submenu>
        <el-menu-item index="4-2"><i class="el-icon-check"></i><span>状态栏</span></el-menu-item>
      </el-submenu>
      <el-submenu index="5">
        <template slot="title">帮助(H)</template>
        <el-menu-item index="5-1" @click="searchHelp">查看帮助</el-menu-item>
        <el-menu-item index="5-2" @click="noteDetails">关于记事本</el-menu-item>
      </el-submenu>
    </el-menu>

      <el-input v-model="input" id="input" :style="{fontSize:postFontSize+'px'}" :class="{inputStyle:inputStyleChange,colorfont:!inputStyleChange}" type="textarea" autosize placeholder="随笔记录"></el-input>
    
    <!--点击新建时，弹出的dialog-->
    <el-dialog title="提示" :visible.sync="dialogNewVisible">
      <span>是否将您写下的内容保存下来？</span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogNewClickSave">保存</el-button>
        <el-button @click="dialogNewClickRemove">不保存</el-button>
      </span>
    </el-dialog>
    <!--点击退出时，弹出的dialog-->
    <el-dialog title="提示" :visible.sync="dialogExitVisible">
      <span>是否将您写下的内容保存下来？</span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogExitClickSave">保存</el-button>
        <el-button @click="dialogExitClickRemove">不保存</el-button>
      </span>
    </el-dialog>
    <!--点击关于记事本，弹出的dialog---记事本详细信息-->
    <el-dialog title="关于记事本" :visible.sync="dialogAboutNote" center>
     <h3>菜单栏：</h3> 
     <h4>1.文件（新建、打开、保存、另存为、退出）</h4>
     <h5>（1）新建：点击后判断文本框是否有内容。若有内容，则弹出对话框询问是否保存。若无内容，则选择路径新建。</h5>
     <h5>（2）打开：选择文件(.txt)打开并将其内容显示在文本框中,仅可读取‘utf-8’编码的txt文件。</h5>
     <h5>（3）保存：选择路径保存</h5>
     <h5>（4）另存为：选择路径保存</h5>
     <h5>（5）退出：判断文本框是否有内容。若有内容，则弹出对话框询问是否保存。若无内容，则退出</h5>
     <h4>2.编辑（撤销、剪切、复制、粘贴、删除）</h4>
     <h5>（1）撤销:仅可撤销删除的数据一次</h5>
     <h5>（2）剪切:复制文本框全部内容+清除文本框全部内容</h5>
     <h5>（3）复制:复制的是文本框的全部内容</h5>
     <h5>（4）粘贴:文本框的内容+要粘贴的内容（即复制的内容或者剪切的内容）</h5>
     <h5>（5）删除:清除文本框全部内容</h5>
     <h4>3.格式（自动换行、改变字体）</h4>
     <h5>（1）自动换行</h5>
     <h5>（2）改变字体:改变字体颜色</h5>
     <h4>4.查看（缩放（放大、缩小、默认缩放）、状态栏）</h4>
     <h5>（1）缩放</h5>
     <h6>（1-1）放大：字体放大</h6>
     <h6>（1-2）缩小：字体缩小</h6>
     <h6>（1-3）默认缩放：默认字体大小16px</h6>
     <h5>（2）状态栏</h5>
     <h4>5.帮助（查看帮助、关于记事本）</h4>
     <h5>（1）查看帮助：浏览器搜索记事本问题</h5>
     <h5>（2）关于此记事本的信息</h5>
     <span slot="footer" class="dialog-footer">
       <el-button @click="dialogAboutNote=!dialogAboutNote">确定</el-button>
     </span>  
    </el-dialog>
  </div>
  
</template>
<script>
import { clipboard } from 'electron';
const {dialog} = require('electron').remote
const fs =require('fs')
export default {
  data() {
    return {
      input: "",
      inputText:'',
      postFontSize:"16",
      inputStyleChange:true,
      dialogNewVisible:false,
      dialogExitVisible:false,
      dialogAboutNote:false,
    };
  },
  created() {},
  methods: {
    //新建
    clickNewNote(){
      let that=this;
      if(this.input && this.input!=''){
        that.dialogNewVisible = true;
      } else{
        dialog.showSaveDialog({
          title:"选择新建路径",
          buttonLabel:"确定",
          filters: [{name: 'All Files', extensions: ['txt'] }]
        },result =>{
          fs.writeFileSync(result,this.input);
        })
      }
    },
    //新建打开的dialog--保存--选择保存路径
    dialogNewClickSave(){
      this.dialogNewVisible=!this.dialogNewVisible;
      dialog.showSaveDialog({
        title:"请选择要保存的路径", 
        buttonlabel:"保存",      
        filters: [
           { name: 'All Files', extensions: ['txt'] }
         ]
      },result =>{
        //console.log(result);
        fs.writeFileSync(result,this.input)
      })
    },
    //新建打开的dialog--不保存--选择新建路径
    dialogNewClickRemove(){
       this.dialogNewVisible=!this.dialogNewVisible;
       dialog.showSaveDialog({
          title:"选择新建路径",
          buttonLabel:"确定",
          filters: [{name: 'All Files', extensions: ['txt'] }]
        },result =>{
          fs.writeFileSync(result,this.input);
        })
    },
    //打开
    clickOpen(){
      let that = this;
      dialog.showOpenDialog({
        title:"选择要打开的文件",
        buttonlabel:"打开",
        filters: [
           { name: 'All Files', extensions: ['txt'] }
         ]
       },result =>{
       // console.log(result[0]);
        fs.readFile(result[0],'utf-8',function(err,data){
          if (err) {
           console.log(err);
          } else {
           console.log(data);
           that.input=data;
          }
        });
      })
    },
    //保存
    clickSave() {
      dialog.showSaveDialog({
        title:"请选择要保存的路径", 
        buttonlabel:"保存",      
        filters: [
           { name: 'All Files', extensions: ['txt'] }
         ]
      },result =>{
        //console.log(result);
        fs.writeFileSync(result,this.input)
      })
      //sessionStorage.setItem("savecontent", JSON.stringify(this.input));
      //console.log(JSON.parse(sessionStorage.getItem("savecontent"))); //将输入内容打印到控制台上
    },
    //另存为
    SaveAnotherPlace() {
      dialog.showSaveDialog({
        title:"请选择要保存的路径", 
        buttonlabel:"保存",      
        filters: [
           { name: 'All Files', extensions: ['txt'] }
         ]
      },result =>{
        //console.log(result);
        fs.writeFileSync(result,this.input)
      })
    },
    //退出
    clickExit(){
      let that=this;
      if(this.input && this.input!=''){
        that.dialogExitVisible = true;
      } else{
        //自定义关闭
        var ipcRender = require('electron').ipcRenderer
        ipcRender.send('handelClose', "执行关闭")
      }
    },
    //退出打开的对话框--保存--选择保存路径
    dialogExitClickSave(){
      this.dialogExitVisible = !this.dialogExitVisible;
       dialog.showSaveDialog({
        title:"请选择要保存的路径", 
        buttonlabel:"保存",      
        filters: [
           { name: 'All Files', extensions: ['txt'] }
         ]
      },result =>{
        fs.writeFileSync(result,this.input)
      })
    },
    //退出打开的对话框--不保存--关闭electron
    dialogExitClickRemove(){
       this.dialogExitVisible = !this.dialogExitVisible;
       var ipcRender = require('electron').ipcRenderer
       ipcRender.send('handelClose', "执行关闭")
    },
    //撤销
    clickBack(){
      this.input=this.inputText;
    },
    //剪切
    clickCut(){
      let that=this;
      this.$copyText(this.input).then(function(e){
        dialog.showMessageBox({
          type: "none",
          title:"提示",
          message:"剪切成功，剪切的内容是"+e.text+"。",
        })
        //console.log(e)
        that.inputText=e.text; 
       //console.log(that.inputText);
        that.input="";
      },function(e){
         dialog.showMessageBox({
          type: "error",
          title:"提示",
          message:"剪切失败",
        })
      })
    },
    //复制
    clickCopy(){
      let that=this;
      this.$copyText(this.input).then(function(e){
        dialog.showMessageBox({
          type: "none",
          title:"提示",
          message:"复制成功，复制的内容是"+e.text+"。",
        })
        that.inputText=e.text;
      },function(e){
        dialog.showMessageBox({
          type: "error",
          title:"提示",
          message:"复制失败",
        })
      })
    },
    //粘贴
    clickPaste(){
      this.input += this.inputText;
    },
    //删除
    clickDelete(){
      this.inputText=this.input;
      this.input='';
    },
    //字体放大
    makeBig(){
      this.postFontSize++;
    },
    //字体缩小
    makeSmall(){
      this.postFontSize--;
    },
    //字体默认
    makeDefault(){
      this.postFontSize=16;
    },
    //查看帮助
    searchHelp(){
      //location.href="https://www.baidu.com/s?wd=记事本问题"
      window.open("http://www.baidu.com/s?wd=记事本问题","_blank")
    },
    //关于记事本--详细信息
    noteDetails(){
      this.dialogAboutNote=!this.dialogAboutNote;
    },
  },
};
</script>
<style lang="scss" scoped>
//输入框样式
.inputStyle{
  font-size: 16px;
  border:0px;
  /deep/ .el-textarea__inner{
    border:0px;
  }
}
//输入框字体-红色
.colorfont{
 /deep/ .el-textarea__inner{
  color:red;
  border:0px;
}
}
</style>