<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1>Quiz App</h1>
      </div>
      <div class="step-progress" :style="{'width':progress + '%'}"></div>
      <div class="quiz-main" v-for="(element,index) in questions.slice(a,b)" :key="index" v-show="quiz">
        <div class="box-question">
          <h2>Question {{b}}/{{questions.length}}</h2>
          <p>{{element.question}}</p>
        </div>
        <div class="box-suggestions">
          <ul>
            <li v-for="(item,index) in element.suggestions" :key="index" :class="select ? check(item) : ''" @click="selectResponse(item)">{{item.suggestion}} <div class="fas fa-check" v-if="select ? item.correct:''"></div> <div class="fas fa-times" v-if="select ? !item.correct:''"></div> </li>
          </ul>
        </div>
      </div>
      <div class="box-score" v-if="score_show">
          <h2>Your score is</h2>
          <h2>{{score}}/{{questions.length}}</h2>
          <div class="btn-restart">
            <button @click="restartQuiz">Restart <i class="fas fa-sync-alt"></i></button>
          </div>
        </div>
      <div class="quiz-footer">
        <div class="box-button" v-if="progress < 100">
          <button @click="skipQuestion" :style="!next ? 'background-color:rgb(106,128,202)' : ''">Skip</button>
          <button @click="nextQuestion" :style="next ? 'background-color:rgb(106,128,202)' : ''">Next</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      questions:[
        {
          question:"汉字中只有一笔的字有几个?",
          suggestions:[
            {suggestion:"1"},
            {suggestion:"2"},
            {suggestion:"3",correct:true},
            {suggestion:"4"},
          ]
        },

        {
          question:"世界最大的半岛",
          suggestions:[
            {suggestion:"朝鲜半岛"},
            {suggestion:"阿拉伯半岛",correct:true},
            {suggestion:"印度半岛"},
            {suggestion:"索马里半岛"},
          ]
        },

        {
          question:"“三北”防护林体系不包括的省区有：",
          suggestions:[
            {suggestion:"黑龙江"},
            {suggestion:"山西"},
            {suggestion:"河南",correct:true},
            {suggestion:"青海"},
          ]
        },

        {
          question:"下列物质属于纯净物的是",
          suggestions:[
            {suggestion:"玻璃"},
            {suggestion:"蒸馏水",correct:true},
            {suggestion:"漂白粉"},
            {suggestion:"空气"},
          ]
        },

        {
          question:"夏天被蚊虫的叮咬时，用 ( )可以迅速止痒。",
          suggestions:[
            {suggestion:"盐"},
            {suggestion:"醋"},
            {suggestion:"酱油"},
            {suggestion:"浓肥皂",correct:true},
          ]
        },

      ],

      a:0,
      b:1,
      select:false,
      score:0,
      quiz:true,
      score_show:false,
      next:false,
      progress:0
    }
  },
  methods:{

    selectResponse(e)
    {
      this.select = true;
      this.next = true;
      if(e.correct){
        this.score++;
      }
    },

    check(status){
      if(status.correct){
        return "correct"
      }else{
        return "incorrect"
      }
      
    },

    nextQuestion(){
      if(!this.next){
        return;
      }

      this.progress = this.progress + (100/this.questions.length);

      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;
      }else{
        this.a++;
        this.b++;
        this.select = false;
        this.next = false;
      }
    },

    skipQuestion(){

      if(this.next){
        return;
      }

      this.progress = this.progress + (100/this.questions.length);

      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;
      }else{
        this.a++;
        this.b++
      }
    },

    restartQuiz(){
      Object.assign(this.$data,this.$options.data());
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
</style>
