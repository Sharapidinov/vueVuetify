<template>
    <div class="input__box">
      <label v-if="config.prefix.show" :style="config.prefix.style">{{ config.prefix.text }}</label>
      <v-select
  :items="selectData"
  :placeholder="config?.placeholder"
  v-model="selectedValue"
  :label="config.label"
  :variant="config.typeInput"
  :item-title="config.keyNLS"
  :item-value="config.key"
  @change="handleChange"
/>
      <p>Выбранное значение: {{ selectedValue }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      config: Object,
      selectData: Array,
      value: Object,
    },
    data() {
      return {
        selectedValue: null,
      };
    },
    methods: {
      handleChange() {
        this.$emit("change", this.selectedValue);
      },
    },
  };
  </script>
  
  <style>
  .input__box {
    width: 50%;
    margin: 0 auto;
  }
  </style>
  