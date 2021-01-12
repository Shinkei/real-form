<template>
  <real-digital-form
    action="http://localhost/post"
    method="POST"
    @onResponse="onResponse"
  >
    <template #="{ store }">
      <real-digital-textfield name="name" validation="[a-z]+" @store="store" />
      <real-digital-textfield name="phone" validation="[0-9]+" @store="store" />
      <real-digital-textfield name="subject" @store="store" />
      <real-digital-button>Send</real-digital-button>
    </template>
  </real-digital-form>
  <div class="response" v-show="showResponse">
    <h5>Response</h5>
    <pre class="response__pre">{{ serverReponse }}</pre>
  </div>
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
  data() {
    return {
      serverReponse: "",
      showResponse: false,
    };
  },
  methods: {
    /**
     * event that print the response of the form in the console and show for 5 seconds
     * the formated response below the form to give some feedback to the user about
     * the interaction
     */
    onResponse(response, status) {
      console.log(response);
      if (status === "success") {
        this.serverReponse = JSON.parse(response.data);
      } else {
        this.serverReponse = response;
      }
      this.showResponse = true;
      setTimeout(() => (this.showResponse = false), 5000);
    },
  },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
}
.response__pre {
  margin-top: 24px;
}
.response {
  display: flex;
  align-items: center;
  flex-direction: column;
}
</style>
