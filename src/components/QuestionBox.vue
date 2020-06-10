<template>

      <div class="quest-container"> 
  <b-jumbotron>
   

    <template v-slot:lead>
            
            <div v-if="currentQuestion" v-html="currentQuestion.question"></div>
    </template>

    <hr class="my-4">
    <div v-if="answers.length > 0">

        <div v-bind:key="index" v-for="(answer,index) in answers">
            <Answer :ind="index" :selected="selected" :selectedIndex="selectedIndex" :handleSelect="handleSelect" :correct="answer===currentQuestion.correct_answer"  :answer="answer"/>

        </div>

                
    </div>
  </b-jumbotron>
</div>

</template>

<script>
import Answer from './Answer'
export default {
 name :'QuestionBox',
 components : {
     Answer
 },
 props : ["currentQuestion","next","selected","selectedIndex","handleSelect"]
 
 ,computed:{
    answers()
    {
        if (this.currentQuestion)
        {
 const {correct_answer , incorrect_answers} = this.currentQuestion
     let answers=[correct_answer , ...incorrect_answers]
     answers=this.shuffle(answers)
     return answers
        }
        return []

    }
  },
  methods : {
      shuffle(array)
      {
        
  var currentIndex = array.length, temporaryValue, randomIndex;

  // While there remain elements to shuffle...
  while (0 !== currentIndex) {

    // Pick a remaining element...
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex -= 1;

    // And swap it with the current element.
    temporaryValue = array[currentIndex];
    array[currentIndex] = array[randomIndex];
    array[randomIndex] = temporaryValue;
  }

  return array;

      }
  }
 
 }
</script>

<style scoped>
        .quest-container
        {
            display: flex;
            justify-content: center;

        }
</style>