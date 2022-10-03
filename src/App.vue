<template>
 <h1>Veille techno</h1>
  <FormVue @add="saveTechno"/>
  <br>
  <TechnoList :technos="technos" @delete-techno="deleteTechno" @edith-techno="editTechno"/>
<!-- ici on test s'il y a plus d'une techno alors un s apparaitra -->
  <p>{{ technos.length }} techno{{technos.length>1? "s":""}}</p>

  <ComponementA/>
</template>

<script>
import FormVue from "@/components/FormVue";
import TechnoList from "@/components/TechnoList";
import ComponementA from "@/components/ComponementA";
import {ref} from "vue";

export default {
  name: 'App',
  components: {
    ComponementA,
    FormVue,
    TechnoList

  },
  setup(){
    let technos = ref([]);
    const saveTechno = function (data) {

      technos.value = [...technos.value, {techno: data, id : technos.value? technos.value.length+1 : 1}]
      console.log("App | saveTechno() | technos.value", technos.value);
    }
    const edithTechno = function (tech){
      technos.value = technos.value.map(t => t.id !== tech.id ? t : tech)
    }
    const deleteTechno = function (tech){
      technos.value= technos.value.filter(t=> t.id !== tech.id)
    }
    return {
      saveTechno,
      technos,
      deleteTechno,
      edithTechno
    }

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
