<template>
  <form @submit.prevent="addTechno">
    <label for="techno">techno à ajouter</label>
    <br>
    <input type="text" name="techno" v-model="techToLearn">
    <br>
    <button type="submit">ajouter</button>
  </form>
</template>

<script>
import {ref} from "vue";

export default {
  setup(props, context){
    let techToLearn=ref("");

    const addTechno = function () {
      console.log("Form | addTechno() | techToLearn", techToLearn.value);
      context.emit("add", techToLearn.value)
      techToLearn.value="";
    }

    return {
      techToLearn,
      addTechno
    }
  }
}
</script>

<style>

</style>