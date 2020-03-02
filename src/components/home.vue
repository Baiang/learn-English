<template>
  <div>
    <p>{{index+1}}/{{zh.length}}</p>
    <p class="f-tit">{{type == "en" ? en[index] : zh[index]}}</p>
    <el-button-group>
  <el-button type="primary" icon="el-icon-arrow-left" @click="previous">上一页</el-button>
      <el-button type="primary" icon="el-icon-reading" @click="read">朗读</el-button>
    <el-button type="primary" icon="el-icon-view" @click="view">{{viewmsg}}</el-button>
  <el-button type="primary" @click="next">下一页<i class="el-icon-arrow-right el-icon--right"></i></el-button>
</el-button-group>
<div v-html="dictVoice">
</div>

  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      index: 0,
      type : "zh",
      en: ["I am eating an apple", "Have you had meal?"],
      zh: ["我正在吃苹果", "你吃过饭了吗？", "你一天吃几顿饭？", "sherry喜欢吃香蕉。", "她不喜欢吃苹果。","你正在吃肉吗？","我见过苹果，我很喜欢吃它，我3点刚吃了一个。","我不吃饭因为我吃过了。", "我正在变胖。", "当时她正在看电视。","你当时正在吃饭吗？是的，我当时是。", "你在上课吗？是的，我在上。", "你不是正在变胖吗？不，我没有。", "你那时不是在想我吗？不，我没在想。", "他已去了伦敦。", "他已经完成了工作。", "我在那里上过学，所以我见过她。", "昨天我看到她的时候，她正在吃苹果。", "你见过她吗？不，我没见过。", "你认识他五年了吗？是的，我是认识他五年了。", "你不是吃过饭了吗？", "他不想学习。", "很多美国人以前不说中文，但是他们现在说了。", "你是想死吗？", "你是想死。", "不要去那里，你是想死吗？我可不想死。", "我妈常说：不要喝可乐。",  "我不想吃饭，因为我刚吃了个苹果。", "别叫我吃饭，我吃过了。", "你不是正在上课吗？是的，我正在上。", "你不是吃过饭了吗？没有，我没吃过。"],
      viewmsg: "查看原文",
      dictVoice: "",
      voiceLink: "https://fanyi.baidu.com/gettts?lan=zh&amp;text=我不吃苹果&amp;spd=5&amp;source=web"
    }
  },
  methods: {
    view(){
      if(this.type == "en"){
        this.type = "zh"
        this.viewmsg = "查看原文"
      }else{
         this.type = "en"
         this.viewmsg = "隐藏原文"
      }
    },
    read(page){
      this.dictVoice = ''
        setTimeout(()=>{
          if(page == "next"){
           var text = this.zh[this.index]
           var lan = "zh"
          }else{
            var text = this.en[this.index]
            var lan = "en"
          }
          this.dictVoice =`
        <audio  autoplay="autoplay" style="display: none;" src="https://fanyi.baidu.com/gettts?lan=${lan}&amp;text=${text}&amp;spd=5&amp;source=web" controls ref='videoPlay' id="dictVoice">
        </audio>
      `
      },100)
    },
    next(){
      if (this.index < this.zh.length-1){
        this.type = "zh"
        this.index++
        this.read("next")
      }
    },
    previous(){
      if (this.index > 0){
        this.type = "zh"
        this.index--

      }
    }
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .f-tit{
    height: 50px;
    line-height: 50px;
    font-size: 18px;
  }
@media screen and (max-width: 375px) {
    .el-button {
        padding: 12px 12px;
    }
}
</style>
