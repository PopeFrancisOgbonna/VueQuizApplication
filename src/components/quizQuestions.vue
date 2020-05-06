<template>
  <div>
      <div>
        <b-jumbotron>
            <template v-slot:lead>Question Counter: {{numCorrect}}/{{numTotal}}</template>
             {{currentQuestion.question}}

            <hr class="my-4">

            <b-container>
              <b-row>
                <b-col sm="fluid" offset="5">
                  <b-list-group >
                    <b-list-group-item class="items" 
                      :key='index' v-for="( answer,index) in answers" 
                      @click="selected(index)"
                      :class="answerClass(index)"
                    >
                      {{answer}}
                    </b-list-group-item>
                  </b-list-group>
                </b-col>
              </b-row>
            </b-container>
            

            <b-button class="btn" variant="primary" @click="submitAnswer" 
              :disabled="selectedIndex === null || answered"
            >
              Submit Answer
            </b-button>
            <b-button class="btn" variant="success" @click='next'>Next</b-button>
        </b-jumbotron>
      </div>
  </div>
</template>

<script>
import _ from 'lodash';
export default {
  name:'quizQuestions',
  components: {
  },
  data(){
    return{
       selectedIndex:null,
       shuffledAnswers: [],
       correctIndex: null,
       answered: false
    }
  },
  props:{
    currentQuestion:Object,
    next:Function,
    increment:Function,
    numTotal:Number,
    numCorrect:Number
  },
  watch: {
    currentQuestion: {
      //calls the watch method when the component monunt and any time there's a change
      immediate: true,
      handler(){
        this.selectedIndex = null;
        this.answered = false;
        this.shuffledAnswer();
      }
    }
  },
  computed:{
    answers(){
      let answer = [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer];
      return answer;
    }
  },
  methods: {
    selected(index){
      this.selectedIndex = index;
    },
    shuffledAnswer(){
      let answer = [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer];
      this.shuffledAnswers = _.shuffle(answer);
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer);
    },
    submitAnswer(){
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex){
        isCorrect = true;
      }
      this.answered = true;
      this.increment(isCorrect);
    },
    answerClass(index){
      let answerClass = '';
      if (!this.answered && this.selectedIndex === index){
        answerClass = 'selected';
      }else if(this.answered && this.correctIndex === index){
        answerClass = 'correct';
      }else if(this.answered && this.selectedIndex === index && this.correctIndex !== index){
        answerClass = 'wrong';
      }
      return answerClass;
    }
  }
}
</script>

<style scoped>
  .btn{
    margin:15px 10px 0 10px;
  }
  .items:hover{
    background: #c7c7c7;
    cursor: pointer;
  }
  .selected{
    background-color: rgb(25, 188, 252);
  }  
  .correct{
    background-color:rgb(27, 250, 57);
  }
  .wrong{
    background-color:rgba(246, 43, 43, 0.966);
  }
</style>