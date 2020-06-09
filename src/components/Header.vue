<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled>Fancy Quiz App</b-nav-item>
      <b-nav-item disabled>Counter: {{ numberCorrect }} / {{ numberTotal }}</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  props: {
    numberCorrect: {
      type: Number,
    },
    numberTotal: Number,
  }
};
</script>

<style>
</style>