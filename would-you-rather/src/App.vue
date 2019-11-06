<template>
  <div id="app">
    <h1 id="would-you-rather">Would You Rather...</h1>
    <div v-for="question in questions" v-bind:key="question">
      <!--cycles through all the questions individualy-->
      <h2 class="question">
        {{question.question}} <!--desplays the question-->
      </h2>
      <!--Sends the question to would you rather: listens for "answer-changed" to run the answerChanged function -->
      <WouldYouRatherQuestion v-bind:question="question" v-on:answer-changed="answerChanged" />
    </div>
    <!--Sends the responces array to Responces-->
    <Responces v-bind:responces="responces" />
  </div>
</template>

<script>
  import WouldYouRatherQuestion from './components/WouldYouRatherQuestion.vue'
  import Responces from './components/Responces.vue'

export default {
  name: 'app',
  components: {
    WouldYouRatherQuestion,
    Responces
  },
  data() {
    return {
      questions: [
        {
          id: 0,
          question: "be able to move silently or have an incredibly loud and scary voice?",
          answers: [
            "Move silently.",
            "Have a loud and scary voice."
          ]
        },
        {
          id: 1,
          question: "have a room with whiteboard walls that you can draw on or a room where the whole ceiling is one big skylight?",
          answers: [
            "Have hiteboard walls.",
            "Have a ceiling skylight."
          ]
        },
        {
          id: 2,
          question: "have a magic carpet that flies or a see-through submarine?",
          answers: [
            "Have a magic carpet.",
            "Have a transparent submarine."
          ]
        }
      ],
      responces: []
    }
  },
  methods : {
    answerChanged(choice) {
      this.responces.splice(choice[0], 1, choice[1])
      // ^ is a slightly harder to read form of "responces[choice[0]] = choice[1]". Vue isn't capable of realtime updating array[index] = value for some reason, so the splice method becomes nesisary.
    }
  }
}
</script>

<style>
body{
  background-color: mediumpurple;
}
#app {
  width: 75%;
  background-color: azure;
  margin: auto;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#would-you-rather{

}
.question {
 display: inline-block;
}

</style>
