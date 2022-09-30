<!--TechnoList a uniquement pour responsabilité d'afficher une liste et d'émettre au parent le souhait de supprimer
 ou d'editer une technos-->
<template>
  <h3>Toutes les technos à veiller</h3>
  <ul>
    <li v-for="tech in technos" v-bind:key="tech.id">
      <button @click="editTechno(tech)">modif</button>
      <button @click="deleteTechno(tech)">suppr</button>
      <span v-if="technoToEdit !== null && technoToEdit.id === tech.id">
        <!-- si on veut que la touche entrée soit écouter sur le champ text il faut mette @keypress -->
        <input type="text" v-model="technoToEdit.techno" @keydown.enter="save"/>
          <button @click="save" >sauvegarder</button>

      </span>
      <span v-else>{{ tech.techno }}</span>

    </li>

  </ul>
</template>

<script>
import {ref} from "vue";

export default {
  emits:['delete-techno','edit-techno'],
  props:{
    technos: {
      type:Array,
      required:true
    }
  },
  setup(props, {emit}){
    //si on a des variables qui doivent changés on oublie pas de mettre ref, il faut penser à l'import comme cela
    // les variables deviendront réactive
    // testt
    let technoToEdit = ref(null);
    const deleteTechno = function (tech){
      emit('delete-techno', tech);
    };
    const editTechno = function (tech){
      technoToEdit.value = tech;
    };
    const save = function () {
      technoToEdit.value = null;
      emit('edit-techno', technoToEdit.value)
    };
    return{
      deleteTechno,
      editTechno,
      technoToEdit,
      save
    };

  }


}
</script>

<style>
  ul{
    list-style: none;
    width: 50%;
    margin-left: 100px;
    text-align: left;
  }

</style>