<template>
  <button :type="type" class="button">
    <slot>Submit</slot>
  </button>
</template>

<script>
export default {
  name: "realDigitalButton",
  props: {
    type: String,
    default: () => "submit",
  },
};
</script>

<style scoped>
.button {
  font-family: "Roboto";
  cursor: pointer;
  width: 100%;
  border: none;
  background: #4caf50;
  color: #fff;
  margin: 0 0 5px;
  padding: 10px;
  font-size: 15px;
}
</style>