<template>
  <div id="app">
        <div id="logos">
          <img class="logo" src="./assets/media/195 (1).webp" alt="460">
        </div>
        <open-page v-if="page === 1" @next-page="nextPage"></open-page>
        <test-page v-if="page === 2" @to-end="scoreAndMovePage"></test-page>
        <end-page v-if="page === 3" :grade="gradeInTest" @again="restart"></end-page>
        <img class="onScrew " src="./assets/media/onburg.png">
        
         <!-- <img class="littlebubble " src="./assets/media/littlebubble.png"> -->
          <!-- <img class="littlenek " src="./assets/media/littlenek.png"> -->
           <img class="littlewave " src="./assets/media/tank.png">
             <img class="towScrew " src="./assets/media/towburg.png">

  </div>
</template>
 
<script>
import OpenPage from "./components/OpenPage.vue";
import TestPage from "./components/TestPage.vue";
import EndPage from "./components/EndPage.vue";
export default {
  name: "app",
  components: {
    OpenPage,
    TestPage,
    EndPage
  },
      data() {
    return {
      page: 1,
      gradeInTest:0
    }
  },
    methods: {
    nextPage() {
      this.page ++;
      console.log(this.page);
    },
    restart(){
      this.page = 1;
    },
    scoreAndMovePage(grade){
      this.gradeInTest = grade;
      this.page++;
    },
  }
};
</script>

<style>
@font-face {
  font-family: "Gan";
  src: url("./assets/fonts/Gan CLM Bold.ttf");
}
@font-face {
  font-family: "Huninn";
  src: url("./assets/fonts/Huninn-Regular.ttf");
}
@font-face {
  font-family: "RubikDood";
  src: url("./assets/fonts/RubikDoodleTriangles-Regular.ttf");
}
@font-face {
  font-family: "Rubik";
  src: url("./assets/fonts/Rubik-Italic-VariableFont_wght.ttf");
}
@font-face {
  font-family: "RubikDistressed";
  src: url("./assets/fonts/RubikDistressed-Regular.ttf");
}



* {
  user-select: none; 
  font-family: "assistant";
  direction: rtl;
  -webkit-user-select: none;
  font-family: "Rubik";
}

html,
body,
#app {
    width: 100%;
    height: 100%;
    margin: 0;
    overflow: hidden;
    /* background-image: url("./assets/media/finelbg.png");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center center;
    background-attachment: fixed; */
    background: #eec99c;

}

#app{
    position: relative;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
}

  body{
    overflow-x: hidden;
    margin:0;
    width:100vw;
    height:100vh;
  }
  #logos {
    position: fixed;
    top: 0%;
    left: 0%;
    z-index: 2;
    padding: 2%;
    width: 100%;
    display: flex;
    flex-wrap: nowrap;
    flex-direction: row-reverse;
    align-items: flex-end;
    justify-content: flex-start;
  }
  .logo {
    max-width: 100%;
    height: 8vh;
    margin-right: 4%;
  }

  #background-gdud {
    position: fixed;
    color: #f6f0e6;
    opacity: 0.1;
    font-family: "aduma";
    right: 50%;
    margin: 0%;
    bottom: 6%;
    font-weight: bold;
    font-size: 55vw;
    rotate: 270deg;
  }

.line {
    position: absolute;
    top: 0;
    left: 0;

    width: 180px;
    z-index: 1;
}
.littlebubble {
    position: absolute;
    top: 95px;
    left: 250px;
    width: 300px;
    opacity: .8;
    z-index: 0;
}

.littlenek {
    position: absolute;
    top: -10px;
    left: -15px;
    width: 125px;
    -webkit-filter: blur(.3px);
    filter: blur(.3px);
    z-index: 0;
}

.littlewave {
    position: absolute;
    width: 260px;
    top: -10px;
    right: 10px;
    opacity: .75;
    z-index: 0;
}

.onScrew {
    position: absolute;
    width: 150px;
    left: 30px;
    bottom: 45px;
    /* opacity: .65; */
    -webkit-animation: rotateGear 18s linear infinite;
    animation: rotateGear 18s linear infinite;
    z-index: 1;
}

@keyframes rotateGear{

    from{
        transform:rotate(0deg);
    }

    to{
        transform:rotate(360deg);
    }

}

.towScrew {
    position: absolute;
    width: 250px;
    top: 350px;
    right: -90px;
    z-index: 0;
    opacity: 70%;
}
</style>