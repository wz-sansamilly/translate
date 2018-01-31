<template>
  <div id="app">
    <h1>在线翻译</h1>
    <h5>简单 / 易用 / 便捷</h5>
    <Translate v-on:translate="translateText"></Translate>
    <Result :outputText="translateResult"></Result>
  </div>
</template>

<script>
import Translate from './components/Translate';
import Result from './components/Result';

export default {
  name: 'App',
  components:{
    Translate:Translate,
    Result:Result,
  },
  data (){
    return {
      translateResult:'',
    }
  },
  methods:{
    translateText (text, language){
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180124T121141Z.144d41e9e521c8ec.89bd75a40c34d8275dcd6365a4024bed3b13edf7&lang='+language+'&text='+text)
          .then((response)=>{
            this.translateResult = response.body.text[0];
      })
      
    }
  }
}
</script>

<style>
@import '../node_modules/semantic-ui/dist/semantic.min.css'; 
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
