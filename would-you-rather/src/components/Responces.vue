<template>
  <!-- real straight forward component. It desplayes the responces that are given to it by App.vue.-->
  <div>
    <h2 class="responces">
      You Would Rather...
    </h2>
    <ul v-for="responce in responces" v-bind:key="responce">
      <li>
        {{ responce }}
      </li>
    </ul>
  </div>
</template>

<script>
export default{
	name: "Responces",
  props: {
    responces: Array
  }
}
</script>

<style>
  ul {
    width: 25%;
    margin: auto;
  }
</style>