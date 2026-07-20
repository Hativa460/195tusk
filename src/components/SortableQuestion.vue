<template>
  <div id="sortable">

    <div class="question-container">

      <div class="question-header">

        <h2 class="question-title">
          {{ title }}
        </h2>

        <!-- <p class="question-subtitle">
          {{ subtitle }}
        </p> -->

      </div>

      <div>
        
      </div>

      <div class="steps-container">
        <p class="question-subtitle">
          {{ subtitle }}
        </p>
       <div
        v-for="(item,index) in items"
        :key="item"
        class="step"
        :class="stepClass(index)"
        @click="selectStep(index)"
        >

          {{ item }}

        </div>

      </div>

      <button
        class="submit-btn"
        @click="submit"
        v-if="!submitted"
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
  name: "SortableQuestion",
  props: ["questionNum"],

data() {
  return {
    items: [],
    selectedIndex: null,
    submitted: false,
    points: 0
  };
},

  computed: {
    question() {
      return json.sortable[this.questionNum];
    },

    title() {
      return this.question ? this.question.title : "";
    },

    subtitle() {
      return this.question ? this.question.subtitle : "";
    },

    correctList() {
      return this.question ? this.question.correctList : [];
    }
  },

  watch: {
    questionNum() {
      this.loadQuestion();
    }
  },
    mounted() {
    this.loadQuestion();
    },

methods: {
  loadQuestion() {
    this.items = [...this.correctList];
    this.shuffle();

    this.selectedIndex = null;
    this.submitted = false;
    this.points = 0;
  },

  shuffle() {
    do {
      for (let i = this.items.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.items[i], this.items[j]] = [this.items[j], this.items[i]];
      }
    } while (
      this.items.every((item, index) => item === this.correctList[index])
    );
  },

  selectStep(index) {
    if (this.submitted) return;

    if (this.selectedIndex === null) {
      this.selectedIndex = index;
      return;
    }

    const temp = this.items[this.selectedIndex];

    this.$set(this.items, this.selectedIndex, this.items[index]);
    this.$set(this.items, index, temp);

    this.selectedIndex = null;
  },

  submit() {
    this.submitted = true;

    let correct = 0;

    this.items.forEach((item, index) => {
      if (item === this.correctList[index]) {
        correct++;
      }
    });

    this.points = correct*5;
      console.log(correct);
  },

  stepClass(index) {
    if (!this.submitted) {
      return this.selectedIndex === index
        ? "selected"
        : "";
    }

    return this.items[index] === this.correctList[index]
      ? "correct"
      : "wrong";
  },

  nextQuestion() {
    this.$emit("points-updated", this.points);

    setTimeout(() => {
      this.$emit("next-question");
    }, 180);
  }
}
};
</script>
<style scoped>

#sortable {
  margin-top: 22%;
  width: 100%;
  display: flex;
  justify-content: center;
  direction: rtl;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.question-container {
  width: 100%;
  max-width: 400px;
  padding: 20px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.question-header {
  text-align: center;
  /* height: 170px; */
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.question-title {
  color: #5c2d13;
  font-size: 28px;
  font-family: RubikDistressed;
  margin: 0 0 10px;
      font-weight: 300;
}

.question-subtitle {
  color: #6d3b1e;
  font-size: 20px;
  margin-top: 10px;
}

.steps-container {
  text-align: center;
  width: 85%;
  /* margin-top: 20px; */
      border: #ceb394 solid 2px;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 12px 35px rgba(74, 50, 31, 0.45);
    background-color: #ffffff33;
}

.step {
  background: #99a897bd;
  color: white;
  /* border: 3px dashed #5c2d13; */
  border-radius: 16px;
  padding: 18px;
  margin-bottom: 12px;
  font-size: 18px;
  font-weight: bold;
  text-align: center;
  cursor: grab;
  user-select: none;
  transition: .25s;
  box-shadow: 0 4px 10px rgba(92,45,19,.18);
      filter: drop-shadow(5px 0.5px 6px rgba(92, 45, 19, .18));
}

.step:hover {
  transform: translateY(-2px);
  box-shadow: 0 7px 18px rgba(92,45,19,.25);
}

.step:active {
  cursor: grabbing;
  transform: scale(.97);
}

.correct {
  border: 2px solid #28c635 !important;
    background: #99a897;
}

.wrong {
  border: 2px solid #c62828 !important;
    background: #99a897;
}

.submit-btn,
.move-on {
  margin-top: 25px;
     background: #5c7d57;
  color: white;
  border: none;
  border-radius: 12px;
  padding: 10px 40px;
  font-size: 22px;
  font-weight: bold;
  cursor: pointer;
  transition: .2s;
  box-shadow: 0 4px 10px rgba(0,0,0,.18);
}

.submit-btn:hover,
.move-on:hover {
  transform: translateY(-2px);
}

.submit-btn:active,
.move-on:active {
  transform: scale(.92);
  background: #8f5d3e;
}

.submit-btn,
.move-on {
  -webkit-tap-highlight-color: transparent;
}
.selected{
  border:2px solid #7e3a0d;
  box-shadow:0 0 15px rgba(161, 85, 13, 0.219);
}
</style>
