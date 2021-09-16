<template>
  <div class="form">
    <div class="form-head">
      <div class="form-head-title">
        <h2>Регистрация</h2>
      </div>
      <div class="form-head-text">Уже есть аккаунт? <a href="#">Войти</a></div>
    </div>
    <div class="form-body">
      <NameInput :form="formCompleted" />
      <EmailInput :form="formCompleted" />
      <PhoneInput :form="formCompleted" />
      <SelectLang :form="formCompleted" />
      <div class="form-body-checkbox">
        <input @click="onCheckbox" type="checkbox" id="confirm" />
        <label for="confirm"> Принимаю <a href="#">условия</a> использования</label>
      </div>
    </div>
    <div v-if="formNotComplete" class="form-input-error">Проверьте поля</div>
    <div class="form-submit">
      <button @click="submit" :class="{ formSubmitBtn: true, active: checked }">
        Зарегистрироваться
      </button>
    </div>
  </div>
</template>

<script>
import NameInput from "../components/NameInput";
import EmailInput from "../components/EmailInput";
import PhoneInput from "../components/PhoneInput";
import SelectLang from "../components/SelectLang";
export default {
  name: "Form",
  data() {
    return {
      formCompleted: {
        nameConfirmed: false,
        emailConfirmed: false,
        phoneConfirmed: false,
        langConfirmed: false,
      },
      checked: false,
      formNotComplete:false
    };
  },
  components: {
    NameInput,
    EmailInput,
    PhoneInput,
    SelectLang,
  },
  methods: {
    onCheckbox() {
      this.checked = !this.checked;
      console.log(this.checked);
    },
    submit() {
      if (this.checked === false) return;

      Object.values(this.formCompleted).find( item=>{
        if(item!==true){
          this.formNotComplete=true
          return true
        }
        else{
           this.formNotComplete=false
           return false
        }
      })
      console.log(this.formCompleted)
    },
  },
  watch: {
    formCompleted(){
      this.formCompleted
    }
  },
};
</script>


