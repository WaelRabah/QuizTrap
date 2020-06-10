<template>
  <div>
      <Header :score="score" :category="questions[0] && questions[0].category" />
      <b-container class="bv-example-row quest-container">
  <b-row>
    <b-col sm="6" offset="3">
      <div v-if="index <= 9">
        <QuestionBox 
        :currentQuestion="questions[index]"
        :next="next"
        :handleSelect="handleSelect"
        :selected="selected"
        :selectedIndex="selectedIndex"
         />
       </div>
       <div v-else>
       <b-jumbotron>

    <hr class="my-4">
    <div class="score">

            <b>Score : {{score}}</b>

                
    </div>
  </b-jumbotron>
         </div>  
    </b-col>
  </b-row>
</b-container>

  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
export default {
  name: 'App',
  components: {
    Header ,
    QuestionBox
  },
  data : ()=>{
 
    return{
    questions : [],
    index : 0,
    selected : false ,
    selectedIndex : -1,
    score : 0
  }
  },
  methods : {
    next()
    {
      this.index++
      this.selected=false;
      this.selectedIndex=-1
    },
      handleSelect (index,correct)
          {
            this.selected=true;
            this.selectedIndex=index
            if(correct)
            {
              this.incremectScore()
            }
            setTimeout(this.next ,1000)

          },
    incremectScore()
    {
      this.score++
    }
  }
  ,
  mounted ()
  {
     fetch('https://opentdb.com/api.php?amount=10&type=multiple')
    .then(response=>response.json())
    .then(({results})=>this.questions=results)
    .catch(err=>console.log(err))
  }
}
</script>

<style>
.score
{
  text-align: center;
}
</style>
