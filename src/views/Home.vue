<template>
    <div>
    <h1>Welcome to My Vue App</h1>
  
    <custom-select
      :config="baseConfig"
      :select-data="singleSelectData"
      :value="singleSelectedValue"
      @change="handleFirstLevelChange"
    ></custom-select>

    <custom-select
      :config="baseConfig"
      :select-data="relatedGroups"
      :value="selectedSubgroupValue"
      @change="handleSubgroupChange"
    ></custom-select>

    <custom-select
      :config="baseConfig"
      :select-data="selectedSubgroupValue ? selectedSubgroupValue.subGroup : []"
      :value="relatedGroupsSelectedValue"
      :disabled="!selectedSubgroupValue"
      @change="handleSecondLevelChange"
    ></custom-select>



    </div>
</template>
  
<script>
import CustomSelect from "../components/CustomSelect.vue";

export default {
    components: {
      CustomSelect,
    },
    methods: {
        handleFirstLevelChange(newValue) {
      // Обработка выбора значения в первом инпуте
      this.singleSelectedValue = newValue;
      this.selectedSubgroupValue = null; // Обнуляем выбранное значение второго уровня при выборе первого уровня
    },

    handleSubgroupChange(newValue) {
      // Обработка выбора значения во втором инпуте
      this.selectedSubgroupValue = newValue;
    },

    handleSecondLevelChange(newValue) {
      // Обработка выбора значения в третьем инпуте
        this.relatedGroupsSelectedValue = newValue
    },
    },
    data() {
      return {
        singleSelectedValue: null,
        relatedGroupsSelectedValue: null,
        selectedSubgroupValue: null,
        baseConfig: {
          typeInput: "underlined",
          label: "input:",
          valueKey: "key",
          labelKey: "keyNLS",
          subGroupKey: "subGroup",
          required: "false",
          prefix: {
            show: "true",
            style: "",
            text: "",
            minWidth: "90px",
            width: "",
            align: "left",
          },
          placeholder: "",
          width: "200px",
          initWithFirstValue: "true",
          class: "",
        },
        singleSelectData: [
          {
            key: "M",
            keyNLS: "Metal",
          },
          {
            key: "P",
            keyNLS: "Plastic",
          },
          {
            key: "C",
            keyNLS: "Composite",
          },
        ],
        relatedGroups: [
          {
            key: "01",
            keyNLS: "CILINDRIC PUMP",
            subGroup: [
              { key: "1", keyNLS: "Type 1" },
              { key: "2", keyNLS: "Type 2" },
              { key: "3", keyNLS: "Type 3" },
              { key: "4", keyNLS: "Type 4" },
            ],
          },
          {
            key: "02",
            keyNLS: "JUNCTION",
            config: {
              type: "select",
              prefix: {
                text: "Material:",
              },
            },
            subGroup: [
              { key: "0", keyNLS: "(Generic)" },
              {
                key: "1",
                keyNLS: "Adapters",
                subGroup: [
                  { key: "M", keyNLS: "Metal" },
                  { key: "P", keyNLS: "Plastic" },
                  { key: "C", keyNLS: "Composite" },
                ],
              },
              { key: "2", keyNLS: "Elbow" },
            ],
          },
          {
            key: "03",
            keyNLS: "VALVE",
            subGroup: [
              { key: "1", keyNLS: "1/2\"" },
              { key: "2", keyNLS: "3/4\"" },
              { key: "3", keyNLS: "1\"" },
              { key: "4", keyNLS: "1 1/2\"" },
              { key: "5", keyNLS: "2\"" },
              { key: "8", keyNLS: "TABLED" },
              { key: "9", keyNLS: "ACCESSORIES" },
            ],
          },
          {
            key: "10",
            keyNLS: "ELECTRICAL RESISTOR",
            subGroup: [
              { key: "0", keyNLS: "(Generico)" },
            ],
          },
          {
            key: "11",
            keyNLS: "Non-Return valve",
            subGroup: [
              { key: "1", keyNLS: "1/2\"" },
              { key: "2", keyNLS: "3/4\"" },
              { key: "3", keyNLS: "Others" },
            ],
          },
          {
            key: "12",
            keyNLS: "Shieldings",
            subGroup: [
              { key: "0", keyNLS: "(Generico)" },
            ],
          },
        ],
      };
    },
  };
  </script>
  
  <style scoped>
  /* Стили для этой страницы (если необходимо) */
  </style>
  