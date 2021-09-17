<template>
  <div class="form-input">
    <div class="form-input-title">Имя</div>
    <div v-if="nameError" class="form-input-error">Заполните правильно поле</div>
    <div class="form-input-text">
      <input v-model="name" placeholder="Введите Ваше имя" />
    </div>
  </div>
</template>

<script>
export default {
  name: "NameInput",
  props: ["form"],
  data() {
    return {
      name: null,
    };
  },
  computed: {
    nameError() {
      return !this.form.nameConfirmed;
    },
  },
  methods: {
    setNameError(value) {
      this.form.confirmed = value;
    },
  },
  watch: {
    name() {
      const regex = /^[a-zа-яё\s]+$/iu; //eslint-disable-line
      if (regex.test(this.name)) {
        console.log("только буквы");
        this.form.nameConfirmed = true;
        this.setNameError(true);
      } else {
        console.log("не только буквы");
        this.form.nameConfirmed = false;
      }
    },
  },
};
</script>
