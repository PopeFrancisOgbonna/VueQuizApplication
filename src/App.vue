<template>
  <div id="app" class="container">
    <Header/>
    <quizQuestions 
      v-if='questions.length'
      :currentQuestion='questions[index]'
      :next='next'
      :numCorrect='numCorrect'
      :numTotal='numTotal'
      :increment='increment'
     />
  </div>
</template>

<script>
import quizQuestions from './components/quizQuestions.vue';
import Header from './components/Header.vue';

export default {
  name: 'App',
  components: {
    quizQuestions,
    Header
  },
  data(){
    return{
      index:0,
      questions:[],
      numCorrect:0,
      numTotal:0
    }
  },
  methods: {
    next(){
      if (this.index < 10){
        this.index++;
      }
    },
    previous(){
      if (this.index > 0){
        this.index--;
      }
    },
    increment(isCorrect){
      if (isCorrect){
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=18&type=multiple',{
      method:'get'
    }).then(Response => {
      return Response.json();
    }).then((jsonData) => {
      this.questions = jsonData.results;
    })
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
