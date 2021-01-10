<template>
  <div>
    <form
      @submit.prevent="submitForm"
      class="form"
      :action="action"
      :method="method"
    >
      <slot @updateForm="upadteForm"></slot>
    </form>
  </div>
</template>

<script>
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
    },
    method: {
      type: String,
      default: "GET",
    },
  },
  methods: {
    submitForm(e) {
      console.log(e);
    },
    updateForm() {
      console.log("upadteForm");
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