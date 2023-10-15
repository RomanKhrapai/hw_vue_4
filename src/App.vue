
<template>
  <div class="body-box" :class="{ 'night-box': !isLight }">
    <DateList :isLight="isLight" />
    <h3>форма яка приймає лише числа</h3>
    <SearchForm class="form" :isLight="isLight" @setError="setError" @setNum="setNum"> </SearchForm>
    <Text v-if="numberFromFormSubmit">Ви ввели число зі значенням: {{ numberFromFormSubmit }}</Text>
    <Text class="error-text" v-if="errorMessage">Валідація повернула помилку: {{ errorMessage }}</Text>
    <RandomList class="random-margin" :class="{ 'night-border': !isLight }" />
    <CustomButton class="animation-btn" :class="{ 'animation-btn-active': isActive, 'night-btn': !isLight }"
      @click="() => { isActive = !isActive }"> при натисненні змінює розмір</CustomButton>
    <button class="theme-btn" @click="toggleTheme" :class="{ 'night-btn': isLight }">Змінити тему</button>
    <Table :isLight="isLight"></Table>
    <ListsWithLastTasks :isLight="isLight" />
  </div>
</template>
<script>
import CustomButton from './components/CustomButton.vue'
import DateList from './components/DateList.vue';
import SearchForm from './components/SearchForm.vue';
import Text from "./components/Text.vue";
import RandomList from "./components/RandomList.vue";
import Table from "./components/Table.vue"
import ListsWithLastTasks from './components/ListsWithLastTasks.vue'


export default {

  components: {
    CustomButton, DateList, SearchForm, Text, RandomList, Table, ListsWithLastTasks
  },
  data() {
    return {
      numberFromFormSubmit: null,
      errorMessage: null,
      isActive: false,
      isLight: true,
    }
  },
  methods: {
    setNum(num) {
      this.errorMessage = null;
      this.numberFromFormSubmit = num;
    },
    setError(message) {
      this.errorMessage = message;
      this.numberFromFormSubmit = null;
    },
    toggleTheme() {
      this.isLight = !this.isLight;
    },
  }
}

</script>

<style scoped>
.error-text {
  background-color: rgba(165, 42, 42, 0.4);
}

.animation-btn {
  transition: transform 1s;
  transform: scale(1);
  margin-bottom: 10px;
}


.animation-btn-active {
  transform: scale(1.5);

}

.theme-btn {
  position: absolute;
  top: 10px;
  right: 10px;
}

.night-box {
  background-color: rgb(47, 45, 45);
  color: bisque;
}

.night-btn {
  background-color: rgb(8, 56, 8);
  color: #ffffff;
  border: 1px solid #fff;
}

.night-border {
  border: 1px solid #fff;
}

.body-box {
  padding: 40px;
  min-height: 100vh;
  box-sizing: border-box;
}

.form {
  margin-bottom: 7px;
}

.random-margin {
  margin-bottom: 15px;
}
</style>
