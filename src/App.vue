<template>
  <div id="app">
    <CustomSelect
      :options="options"
      :selectedValue="selectedValue"
      :placeholder="placeholder"
      :onChange="handleChange"
    />
    <CustomTable />
    <p>{{ selectedValue ? 'Значение выбрано, селект закрыт' : ''}}</p>
  </div>
</template>

<script>
import CustomSelect from './components/CustomSelect/CustomSelect.vue';
import CustomTable from './components/CustomTable/CustomTable.vue';

export default {
  name: 'App',
  components: {
    CustomSelect,
    CustomTable
  },
  data() {
    return {
      options: [
        { id: 1, title: 'Слон' },
        { id: 2, title: 'Бегемот' },
        { id: 3, title: 'Зебра' },
        { id: 4, title: 'Жираф' },
        { id: 5, title: 'Лев' },
      ],
      selectedValue: null,
      placeholder: 'Выберите значение',
    }
  },
  methods: {
    handleChange(selectedOption) {
      this.selectedValue = selectedOption;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
