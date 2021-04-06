<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-md-8 offset-md-2 mt-5 text-center">
        <h1>A Simple Mini Quiz</h1>
      </div>
    </div>
    <hr />
    <div class="row">
      <div class="col-xs-12 col-md-8 offset-md-2 mt-5">
        <transition name="flip" mode="out-in">
          <component
            :is="mode"
            @confirmed="mode = 'app-question'"
            @btnAnswer="btnAnswer($event)"
          ></component>
        </transition>
      </div>
    </div>
  </div>
</template>
<script>
import Question from './components/question.vue';
import Answer from './components/answer.vue';

export default {
  data() {
    return {
      mode: 'app-question',
    };
  },
  methods: {
    btnAnswer(correct) {
      if (correct) {
        this.mode = 'app-answer';
      } else {
        this.mode = 'app-question';
        // alert('Its Wrong!! Try again');
      }
    },
  },
  components: {
    appQuestion: Question,
    appAnswer: Answer,
  },
};
</script>

<style scoped>
.flip-enter-active {
  animation: flips .5s ease-out forwards;
}
.flip-leave-active {
  animation: flips .5s ease-out reverse;
}
@keyframes flips {
  from {
    transform: rotateY(90deg);
  }
  to {
    transform: rotateY(0deg);
  }
}
</style>
