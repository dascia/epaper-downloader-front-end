<template>
  <div class="edition-selection-container">
    <span class="edition-indication">Select the date of the edition wanted</span>
    <input class="calendar" type="date" v-model="selectedDate" @change="editionSelected" />
  </div>
</template>
<script lang="ts">
import { ref } from 'vue';
export default {
  name: 'edition-selector',
  setup(props, { emit }) {
    // new Date().toISOString().slice(0,10)
    const selectedDate = ref<string>('');
    const emits = ['edition-selected'];
    // Function executed when the edition control date changes
    function editionSelected() {
      console.log('Selected date: {0}', selectedDate.value);
      emit('edition-selected', selectedDate.value);
    }

    // return
    return {
      selectedDate,
      editionSelected,
    };
  },
};
</script>

<style scoped>
.edition-indication {
  font-family: 'Open Sans', sans-serif;
  font-size: 0.8em;
  color: gray;
  padding: 10px;
}
.edition-selection-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.calendar {
  width: 180px;
  height: 28px;
  text-align: center;
  border: solid 1px lightgray;
  font-family: 'Open Sans', sans-serif;
}
</style>
