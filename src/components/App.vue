<template>
  <div id="app">
    <div class="title">💟 豚豚翻譯器</div>
    <div class="container-translator">
      <div class="container-text">
        <span class="icon-text">👶</span>
        <el-input
          placeholder="輸入人話"
          class="input"
          type="textarea"
          v-model="humanText"
          :autosize="{ minRows: 2, maxRows: 4}">
        </el-input>
      </div>
      <el-button-group class="container-buttons">
        <el-button class="button-translate-to-dolphin" icon="el-icon-bottom" circle @click="translateToDolphin"></el-button>
        <el-button class="button-translate-to-human" icon="el-icon-top" circle @click="translateToHuman"></el-button>
      </el-button-group>
      <div class="container-text">
        <span class="icon-text">🐬</span>
        <el-input
          class="input"
          type="textarea"
          placeholder="輸入海豚語"
          v-model="dolphinText"
          :autosize="{ minRows: 2, maxRows: 4}">
        </el-input>
      </div>
    </div>
<!--     <div class="fb-page" data-href="https://www.facebook.com/iruka0.0/" data-tabs="" data-width="" data-height="" data-small-header="true" data-adapt-container-width="true" data-hide-cover="false" data-show-facepile="true"><blockquote cite="https://www.facebook.com/iruka0.0/" class="fb-xfbml-parse-ignore"><a href="https://www.facebook.com/iruka0.0/">イルカポリス 海豚刑警</a></blockquote></div> -->
  </div>
</template>
<style>
  
  body{
    height: 100%;
    margin:0;
  }
  html{
    height: 100%;
  }
  .icon-text{
    font-size:25px;
    padding-top:10px;
    margin-right:10px;
  }
  .input{
    width:90%;
  }
  #app{
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 100%;
    padding-bottom:10vh;
    box-sizing: border-box;
    background-color: #eff;
  }
  
  .title{
    align-self:center;
    font-size:24px;
    margin:10px;
    font-family: arial;
  }
  .container-translator{
    display: flex;
    justify-content: center;
    flex-direction: column;
    width:500px;
    align-self:center;
  }
  .container-text{
    display:flex;
    justify-content: space-evenly;
    margin:30px 0;
  }
  .container-text .input textarea{
    border-radius:10px;
  }
  .container-buttons{
    align-self:center;
  }
  .text-copied{
    align-self:center;    
    color:black;
    font-size:10px;
  }
  .fb-page{
    position:fixed !important;
    bottom:0 !important;
    right:0 !important;
    
  }
  @media (max-width: 600px) {
    .container-translator {
      width:90%;
    }
    .fb-page {
      height:0;
      width:0;
      overflow:none;
    }
  }
</style>

<script>
import {tify, sify} from 'chinese-conv';
const rules=[['什麽','什ㄇ'],['自己','痣己'],['海豚刑警','豚丼'],['朋友','bro bro'],['開心','哈皮'],['Ok','O吹'],['ok','o吹'],['那個','那股'],['這個','這股'],
             ['我','婐'],['你','ㄋ'],['妳','ㄋ'],['他','ㄊ'],['們','悶'],['去','ㄑ'],['很','狠'],['嗎','ㄇ'],['不','咘'],['不','ㄅ'],['的','ㄉ'],['了','ㄌ'],['個','ㄍ'],['可','ㄎ'],
             ['啦','喇'],['啦','辣'],['啊','吖'],['啊','ㄚ'],['呢','ㄋ'],['耶','ㄝ'],['喔','ㄛ'],['哈','ㄏ'],['嗯','ㄣ'],['吧','ㄅ'],['呃','ㄜ'],['呦','ㄡ'],
             ['、','、、'],['，',',,'],['，','，，'],['？','？？？'],['！','!'],['！','！！'],
             ['qq','=='],['qwq','0.0'],[':)','^^'],['。。','@@'],['...','@@'],['。。。','@@'],['..','@@'],['XD','=）']];
export default {
  data(){
    return {humanText:"",dolphinText:"",copied:false}
  },
  methods:{
    translateToDolphin(){
      if (this.humanText!==""){
      let text = this.humanText;
      text=tify(text);
      for (let rule of rules){
        text=text.split(rule[0]).join(rule[1]);
      }
      this.dolphinText=text;
      navigator.clipboard.writeText(text).then(()=>{this.$message('複製好了^^!!');},()=>{});
      }
      else{
        navigator.clipboard.readText().then((clip)=>{console.log(clip);this.humanText=clip;this.translateToDolphin();},()=>{console.log('fail')});
      }
    },
    translateToHuman(){
      if (this.dolphinText!==""){
      let text=this.dolphinText;
      for (let rule of rules){
        text=text.split(rule[1]).join(rule[0]);
      }
      this.humanText=text;
      navigator.clipboard.writeText(text).then(()=>{this.$message('複製好了^^!!');},()=>{});
      }
        else{
        navigator.clipboard.readText().then((clip)=>{console.log(clip);this.dolphinText=clip;this.translateToHuman();},()=>{console.log('fail')});
    }}
  }
}
</script>