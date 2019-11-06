<template>
  <div>
    <div class="radio-buttons"
         v-for="answer in question.answers"
         v-bind:key="answer">
      <!--:id is to group the radio button with it's label. :name is to group the pairs of raido buttons.
      on change, emits the question's id and the selected answer. The question ID must be emited so that App.vue can ensure that only one responce per radio pair is being desplayed.-->
      <input type="radio"
             :id="answer"
             :name="question.id"
             v-on:change="$emit('answer-changed', [question.id, answer])"
             v-bind:value="answer" />
      <label :for="answer">
        {{answer}}
      </label>
    </div>
  </div>
</template>

<script>
export default{
	name: "WouldYouRatherQuestion",
  props: {
    question: Object
  }
}
</script>