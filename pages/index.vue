<template>
  <div
    class="mx-0 my-auto min-vh-100 d-flex justify-content-center align-items-center text-align-center"
  >
    <calculator />
  </div>
</template>

<script>
import calculator from "~/components/calculator.vue";

export default {
  components: {
    calculator
  }
};
</script>

<style>
body {
  background-image: url("/mirrored-squares.png");
  /*  Courtesy: https://www.transparenttextures.com/  */
}
</style>