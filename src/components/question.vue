<template>
  <div class="card">
    <div class="card-header">
      <div class="card-title text-center">
        {{ question }}
      </div>
    </div>
    <div class="card-body">
      <div
        class="col-xs-12 col-sm-6 text-center"
        style="display: inline-block"
        v-for="btnData in btnDatas"
      >
        <button
          class="btn btn-primary btn-lg"
          style="margin: 10px"
          @click="answerd(btnData.data)"
        >
          {{ btnData.answer }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      question: "Oops! An error acurred!",
      btnDatas: [
        { answer: 0, data: true },
        { answer: 1, data: false },
        { answer: 2, data: false },
        { answer: 3, data: false },
      ],
    };
  },
  methods: {
    getQuestionNumber() {
      let addition = 1;
      let subtraction = 2;
      let firstNumber = this.getRandomNumber(1, 100);
      let secondNumber = this.getRandomNumber(1, 100);
      let operation = this.getRandomNumber(1, 2);
      let currentNumber = 0;

      switch (operation) {
        case addition:
          currentNumber = firstNumber + secondNumber;
          this.question = `What is ${firstNumber} + ${secondNumber} ?`;
          break;
        case subtraction:
          currentNumber = firstNumber - secondNumber;
          this.question = `What is ${firstNumber} - ${secondNumber} ?`;
          break;

        default:
          currentNumber = 0;
          this.question = "Oops! An error acurred!";
          break;
      }
      for (let i = 0; i < this.btnDatas.length; i++) {
        debugger;
        this.btnDatas[i].data = false;
        let condition = false;
        while (!condition) {
          debugger;
          let wrongAnswer = this.getRandomNumber(
            currentNumber - 5,
            currentNumber + 5,
            currentNumber
          );
          if (
            this.btnDatas.filter((btn) => wrongAnswer === btn.answer).length > 0
          ) {
            debugger;
            condition = false;
          } else {
            this.btnDatas[i].answer = wrongAnswer;
            condition = true;
          }
  
        }
      }

      
      let correctAnswer = this.getRandomNumber(0, 3);
      console.log(correctAnswer);
      this.btnDatas[correctAnswer].answer = currentNumber;
      this.btnDatas[correctAnswer].data = true;
    },

    getRandomNumber(min, max, except) {
      let randNum = Math.round(Math.random() * (max - min)) + min;
      if (randNum == except) {
        return this.getRandomNumber(min, max, except);
      } else {
        return randNum;
      }
    },

    answerd(correct) {
      this.$emit("btnAnswer", correct);
    },
  },
  created() {
    this.getQuestionNumber();
  },
};
</script>

<style scoped>
</style>