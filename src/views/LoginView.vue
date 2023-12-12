<template>
  <LoginForm />
</template>

<script>
import LoginForm from "@/components/LoginForm.vue";

export default {
  components: { LoginForm },
};
</script>

<style>
.form-main-wrapper {
  width: 400px;

  margin: 100px auto;
  padding: 20px 50px;

  text-align: center;

  background-color: transparent;

  overflow: auto;
}

.form-main-title {
  font-size: 32px;
  color: #000;
}

.form-main-label {
  font-size: 24px;
  text-align: start;

  color: #000;
}

.form-main-link-wrapper {
  color: #000;
}

.form-main-link {
  text-decoration: none;

  color: black;
}
</style>
