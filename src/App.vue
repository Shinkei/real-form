<template>
  <real-digital-form action="/script.php" method="POST">
    <real-digital-textfield name="name" validation="[a-z]+" />
    <real-digital-textfield name="phone" validation="[0-9]+" />
    <real-digital-textfield name="subject" />
    <real-digital-button>Send</real-digital-button>
  </real-digital-form>
</template>

<script>
import RealDigitalButton from "./components/RealDigitalButton.vue";
import RealDigitalForm from "./components/RealDigitalForm.vue";
import RealDigitalTextfield from "./components/RealDigitalTextfield";

export default {
  name: "App",
  components: {
    RealDigitalForm,
    RealDigitalTextfield,
    RealDigitalButton,
  },
};
</script>

<style>
#app {
  font-family: Roboto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
