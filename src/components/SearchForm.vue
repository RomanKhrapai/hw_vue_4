<template>
  <form class=form-name @submit.prevent="searchCitys">

    <input class=form-input :class="{ 'night': !isLight }" :value="inputValue" @input="getInputValue" type=text required
      autocomplete=off placeholder='Введіть число' />
    <SearchButton :class="{ 'night': !isLight }">Submit</SearchButton>
  </form>
</template>


<script>

import SearchButton from "./SearchButton.vue";
export default {
  props: ["isLight"],
  emits: ['setNum', 'setError'],
  data() {
    return { inputValue: '', }
  },
  components: { SearchButton },
  methods: {
    getInputValue(e) {
      this.inputValue = e.target.value.replace(/\D/g, "")
      e.target.value = this.inputValue
      console.log(this.islight);
    },
    searchCitys() {
      if (this.inputValue.length < 2) {
        this.$emit('setError', `число ${this.inputValue} менше двох знаків`)
        return
      }
      this.$emit('setNum', +this.inputValue),
        this.inputValue = ''
    }
  }
};
</script>

<style scoped>
.form-name {
  display: flex;
  justify-content: center;
  height: 30px;
  padding: 0;
  margin-right: 10px;
}

.form-input {
  border-radius: 10px 0 0 10px;
  padding-left: 20px;
  border-right: none;
}

.night {
  background-color: rgb(8, 56, 8);
  color: #ffffff;
  border: 1px solid #fff;
}
</style>