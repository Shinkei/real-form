<template>
  <div class="field">
    <input :placeholder="name" v-model="value" class="input" />
    <p v-show="hasError" class="error">invalid value</p>
  </div>
</template>

<script>
export default {
  name: "realDigitalTextfield",
  data() {
    return {
      value: "",
      hasError: false,
    };
  },
  props: {
    name: {
      type: String,
      required: true,
    },
    validation: {
      type: String,
    },
  },
  watch: {
    value() {
      let hasError = false;
      if (this.validation) {
        const reg = new RegExp(this.validation);
        hasError = !reg.test(this.value);
      }
      this.hasError = hasError;
      this.$emit("store", this.name, {
        value: this.value,
        hasError: this.hasError,
      });
    },
  },
};
</script>

<style scoped>
.field {
  border: medium none !important;
  margin: 0 0 10px;
  min-width: 100%;
  padding: 0;
  width: 100%;
}
.input {
  width: 95%;
  border: 1px solid #ccc;
  background: #fff;
  margin: 0 0 5px;
  padding: 10px;
}
.error {
  margin: 0;
  margin-left: 5px;
  font-size: 11px;
  color: red;
  height: 15px;
}
</style>