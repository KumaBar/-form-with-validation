<template>
  <div class="form-input">
    <div class="form-input-title">Email</div>
     <div v-if="emailError" class='form-input-error'>Заполните правильно поле</div>
    <div class="form-input-text">
      <input v-model="email" placeholder="Введите ваш email" />
    </div>
  </div>
</template>

<script>
export default {
  name: "EmailInput",
  props:['form'],
  data() {
    return {
      email: null,
    };
  },
  computed: {
      emailError(){
          return !this.form.emailConfirmed
      }
  },
  watch: {
    email() {
      const regex = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/; //eslint-disable-line
      if (regex.test(this.email)) {
        console.log("email прошел");
        this.form.emailConfirmed = true;
      } else {
        console.log("email не прошел");
         this.form.emailConfirmed = false;
      }
    },
  },
};
</script>

<style>

</style>
