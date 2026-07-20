<template>
  <div id="select-multiple">

    <div class="question-container">

      <div class="question-header">
        <h2 class="question-title">{{ title }}</h2>
        <!-- <p class="question-subtitle">{{ subtitle }}</p> -->
      </div>

      <div class="options-container">
        <p  class="question-subtitle">{{ subtitle }}</p>
        <div
          v-for="(option,index) in options"
          :key="index"
          class="option-card"
          :class="optionClass(index)"
          @click="toggleOption(index)"
        >

          <div class="option-text">
            {{ option }}
          </div>

          <div class="checkbox">

            <span v-if="selected.includes(index)">
              ✔
            </span>

          </div>

        </div>

      </div>

      <button
        class="submit-btn"
        v-if="!submitted"
        @click="submit"
      >
        הגש
      </button>

      <button
        class="move-on"
        v-if="submitted"
        @click="nextQuestion"
      >
        המשך
      </button>

    </div>

  </div>
</template>

<script>
import json from "../../text.json";

export default {

  name:"SelectMultiple",

  props:["questionNum"],

  data(){
    return{
      selected:[],
      submitted:false,
      points:0
    }
  },

  computed:{

    currentQuestion(){
      return json.selectMultiple[this.questionNum];
    },

    title(){
      return this.currentQuestion
        ? this.currentQuestion.title
        : "";
    },

    subtitle(){
      return this.currentQuestion
        ? this.currentQuestion.subtitle
        : "";
    },

    options(){
      return this.currentQuestion
        ? this.currentQuestion.options
        : [];
    },

    correctAns(){
      return this.currentQuestion
        ? this.currentQuestion.correctAns
        : [];
    }

  },

  mounted(){
    this.resetQuestion();
  },

  watch:{
    questionNum(){
      this.resetQuestion();
    }
  },

  methods:{

    toggleOption(index){

      if(this.submitted) return;

      if(this.selected.includes(index)){

        this.selected=this.selected.filter(i=>i!==index);

      }else{

        this.selected.push(index);

      }

    },

    submit(){

      this.submitted=true;

      let score=0;

      this.selected.forEach(index=>{

        if(this.correctAns.includes(index)){

          score+=5;

        }

      });

      this.points=score;

    },

    optionClass(index){

        if(!this.submitted){
            return this.selected.includes(index)
            ? "selected"
            : "";
        }

        const selected = this.selected.includes(index);
        const correct = this.correctAns.includes(index);

        if(selected && correct){
            return "correct";
        }

        if(selected && !correct){
            return "wrong";
        }

        return "";

        },

    nextQuestion(){

      this.$emit("points-updated",this.points);

      setTimeout(()=>{

        this.$emit("next-question");

      },180);

    },

    resetQuestion(){

      this.selected=[];
      this.submitted=false;
      this.points=0;

    }

  }

}
</script>

<style scoped>

#select-multiple{
  margin-top:15%;
  width:100%;
  display:flex;
  justify-content:center;
  direction:rtl;
  font-family:'Segoe UI',Tahoma,Geneva,Verdana,sans-serif;
}

.question-container{
  width:100%;
  max-width:400px;
  padding:20px;
  box-sizing:border-box;
  display:flex;
  flex-direction:column;
  align-items:center;
}

.question-header{
  text-align:center;
  margin-bottom:20px;
  /* height:170px; */
  display:flex;
  flex-direction:column;
  justify-content:center;
}

.question-title{
  color:#5c2d13;
  font-size:28px;
   font-family: RubikDistressed;
  margin:0 0 10px;
      font-weight: 300;
}

.question-subtitle{
    color: #6d3b1e;
    font-size: 17px;
    /* line-height: 1.4; */
    margin-top: 10px;
    text-align: center;
}

.options-container{
  width:80%;
  margin-top:10px;
    background-color: #ffffff33;
    border: #ceb394 solid 2px;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 12px 35px rgba(74, 50, 31, 0.45);
}


.option-card{
  display:flex;
  align-items:center;
  justify-content:space-between;

  background-color:#99a897bd;

  border-radius:18px;

  padding:8px 18px;

  margin-bottom:14px;

  cursor:pointer;

  transition:.2s;

  box-shadow:0 4px 10px rgba(92,45,19,.15);

  border:3px solid transparent;
}

.option-card:active{
  transform:scale(.97);
}

.option-text{
  color:white;
  font-size:15px;
  font-weight:bold;
  width:80%;
}

.checkbox{
  width:24px;
  height:24px;

  border-radius:10px;

  border:3px solid white;

  display:flex;
  justify-content:center;
  align-items:center;

  color:white;
  font-size:22px;
  font-weight:bold;

  flex-shrink:0;
}

.selected{
  border:2px solid #a1480d;
  box-shadow:0 0 15px rgba(161, 85, 13, 0.219);
}

.correct{
  border-color:#2e7d32 !important;
  background:rgba(179,241,160,.95);
}

.correct .option-text{
  color:#000;
}

.correct .checkbox{
  border-color:#2e7d32;
  color:#2e7d32;
  background:white;
}

.wrong{
  border-color:#c62828 !important;
  background:rgba(247,83,83,.95);
}

.wrong .checkbox{
  border-color:white;
}

.submit-btn,
.move-on{

  background-color: #5c7d57;
  color: white;
  font-size: 20px;
  font-weight: bold;
  border: none;
  border-radius: 12px;
  padding: 12px 30px;
  cursor: pointer;

  transition:
    transform .18s ease,
    background-color .18s ease,
    box-shadow .18s ease;

  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);

  -webkit-tap-highlight-color: transparent;
}

.submit-btn:active,
.move-on:active{

  transform:scale(.93);

  background:#8f5d3e;

}

.submit-btn{
  -webkit-tap-highlight-color:transparent;
}

.move-on{
  -webkit-tap-highlight-color:transparent;
}

</style>