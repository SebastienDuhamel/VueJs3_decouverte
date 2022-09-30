<template>
  <h1>Je suis le component A</h1>
  <br>
  <ComponementB/>
  <br>
  <ComponementC/>
  <App/>
</template>

<script>
import ComponementB from "@/components/ComponementB";
import ComponementC from "@/components/ComponementC";

export default {
  components: {ComponementC, ComponementB}
}
</script>

<style>

</style>