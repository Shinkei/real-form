<template>
  <div>
    <form @submit.prevent="submitForm" class="form">
      <slot :store="store"></slot>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "realDigitalForm",
  data() {
    return {
      form: {},
    };
  },
  props: {
    action: {
      type: String,
      required: true,
      default: "/",
    },
    method: {
      type: String,
      default: "GET",
    },
  },
  methods: {
    /**
     * submit the form to the specified server and method, doind a second validation
     * to verify that the input fields has valid data, it uses axios to do the reques.
     * after the request, emit the onResponse event with the response from the server and
     * a string status
     */
    async submitForm() {
      const canSubmit = Object.values(this.form).every(
        (field) => field.hasError === false
      );
      if (canSubmit) {
        const reqForm = Object.entries(this.form).reduce((acc, [key, val]) => {
          acc[key] = val.value;
          return acc;
        }, {});

        try {
          const res = await axios({
            method: this.method,
            url: this.action,
            data: reqForm,
            headers: {
              "content-type": "application/json",
            },
          });
          this.$emit("onResponse", res.data, "success");
        } catch (err) {
          const message = `there was an error sending the data/n${err}`;
          this.$emit("onResponse", message, "fail");
        }
      }
    },
    /**
     * listen to the changes in the children inputs and start creating
     * an object with all the information from the input, value and hasErros
     */
    store(name, value) {
      this.form[name] = value;
    },
  },
};
</script>

<style scoped>
.form {
  width: 500px;
  padding: 12px;
  margin: auto;
  display: flex;
  border-radius: 6px;
  flex-direction: column;
  align-items: center;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2), 0 5px 5px 0 rgba(0, 0, 0, 0.24);
}
</style>