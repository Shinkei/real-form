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
    submitForm() {
      const canSubmit = Object.values(this.form).every(
        (field) => field.hasError === false
      );
      if (canSubmit) {
        const reqForm = Object.entries(this.form).reduce((acc, [key, val]) => {
          acc[key] = val.value;
          return acc;
        }, {});
        try {
          axios({
            method: this.method,
            url: this.action,
            data: reqForm,
          });
        } catch (err) {
          console.log("there was an error sending the data", err);
        }
      }
    },
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