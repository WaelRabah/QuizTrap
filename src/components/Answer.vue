<template>
  <div class="answer" @click="handleSelect(ind,correct)" :class="[selected && showClass] ">
      <div v-html="answer"></div>
  </div>
</template>

<script>
export default {
        name :"Answer",
        props : ["answer","selected","correct","selectedIndex","ind","handleSelect"],
        computed : {
          showClass()
          {
            if (this.selected)
            { 
  if (this.correct)
            {
              return "correct"
            }
      
            if (this.selectedIndex===this.ind)
            {
              
              return "selected"
            }
          
                  }
            return ""
          },
        }

}
</script>

<style scoped>
@keyframes onHover {
  from {
      transform: scale(1.0);
  }
  to
  {
transform: scale(1.05);
  }
}
 .answer
 {
   border: solid 1px gray;
   margin : 2px;
   cursor: pointer;
     background: linear-gradient(to right, #FDB827 50%, white 50%);
  background-size: 200% 100%;
  background-position: right bottom;
  transition: all .5s ease-out;
 }
 .answer:hover
 {
      animation: onHover 0.4s  ;
      transform: scale(1.05);
 }

.selected
{
  background: #900C3F;
}
 .correct
 {

background-position: left bottom;
 }
</style>