<template>
  <div class="form-input">
    <div class="form-input-title">Номер телефона</div>
     <div v-if="phoneError" class='form-input-error'>Заполните правильно поле</div>
    <div  class="form-input-text">
      <input v-model="phonenumber" placeholder="Введите номер телефона" />
    </div>
  </div>
</template>

<script>
export default {
  phonenumber: "EmailInput",
  props:['form'],
  data() {
    return {
      phonenumber: null,
    };
  },
  computed: {
      phoneError(){
          return !this.form.phoneConfirmed
      }
  },
  watch: {
    phonenumber() {
      const regex = /^(\+7|7|8)?[\s\-]?\(?[489][0-9]{2}\)?[\s\-]?[0-9]{3}[\s\-]?[0-9]{2}[\s\-]?[0-9]{2}$/; //eslint-disable-line
      if (regex.test(this.phonenumber)) {
        console.log("телефон прошел");
        this.form.phoneConfirmed = true;
      } else {
        console.log("телефон не прошел");
          this.form.phoneConfirmed = false;
      }
    },
  },
};
</script>
