<template>
  <div class="form-select">
    <div class="form-select-title">Язык</div>
       <div v-if="langError" class='form-input-error'>Заполните правильно поле</div>
    <button :class="{ formSelectBtn: true, active: isOpen }" @click="open">
      {{ currentLang.lang }}
      <span>
        <img src="../assets/angle-arrow-down_icon-icons.com_73683.svg" alt=""
      /></span>
    </button>
    <div :class="{ formSelectPanel: true, active: isOpen }">
      <div
        @click="changeLang(item.id)"
        :class="{ formSelectPanelItem: true }"
        v-for="item in items"
        :key="item.id"
      >
        {{ item.lang }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SelectLang",
  props: ["form"],
  data() {
    return {
      isOpen: false,
      currentLang: { lang: "Язык" },
      items: [
        { id: 1, lang: "Русский" },
        { id: 2, lang: "Китайский" },
        { id: 3, lang: "Английский" },
        { id: 4, lang: "Испанский" },
      ],
    };
  },
  methods: {
    open() {
      this.isOpen = !this.isOpen;
      console.log(this.isOpen);
    },
    changeLang(id) {
      this.items.find((item) => {
        if (id === item.id) {
          this.currentLang = item;
          this.isOpen = !this.isOpen;
          return true;
        }
      });
    },
  },
  computed: {
      langError(){
          return !this.form.langConfirmed
      }
  },
  watch: {
    currentLang() {
      if (this.currentLang.id) {
        this.form.langConfirmed = true;
      } else {
         this.form.langConfirmed = false;
      }
    },
  },
};
</script>

<style>
.form-select {
  position: relative;
  margin-bottom: 20px;
}
.form-select-title {
  margin-bottom: 5px;
}
.formSelectBtn {
  width: 100%;
  border: 1px solid grey;
  border-radius: 5px;
  background: none;
  text-align: left;
  padding: 10px;
  font-size: 16px;
  color: grey;
  position: relative;
}
.formSelectBtn span {
  position: absolute;
  right: 10px;
  top: 10px;
  transition: 0.2s;
}
.formSelectBtn span img {
  width: 20px;
}
.formSelectBtn.active span {
  transform: rotateZ(180deg);
  top: 5px;
}
.formSelectPanelItem {
  padding: 10px;
  background: white;
  transition: 0.2s;
}
.formSelectPanelItem:hover {
  background: grey;
}
.formSelectPanel {
  max-height: 0;
  position: absolute;
  overflow: hidden;
  transition: all 0.2s;
  z-index: 2;
  margin-top: 5px;
  width: 100%;
  cursor: pointer;
  border-radius: 5px;
}
.formSelectPanel.active {
  display: block;
  max-height: 200px;
  box-shadow: 4px 4px 8px 6px rgba(34, 60, 80, 0.2);
}
</style>
