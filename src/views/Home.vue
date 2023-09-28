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
            v-if="selectedSubgroupValue && selectedSubgroupValue.subGroup"
            :config="baseConfig"
            :select-data="selectedSubgroupValue.subGroup"
            value="relatedGroupsSelectedValue"
            @change="handleSubgroupChange"
        ></custom-select>
    </div>
</template>


<script>
import CustomSelect from "../components/CustomSelect.vue"; // Импортируйте ваш компонент CustomSelect

export default {
    components: {
        CustomSelect, // Регистрируем ваш компонент CustomSelect
    },
    methods: {
        handleFirstLevelChange(newValue) {
            console.log(newValue)

            this.singleSelectedValue = newValue;
            this.selectedSubgroupValue = null; // Обнуляем выбранное значение второго уровня при выборе первого уровня
        },
        handleSubgroupChange(newValue) {
            this.selectedSubgroupValue = newValue;
            console.log(newValue)
        },
        handleSecondLevelChange(newValue) {
            // Обработка выбора значения во втором инпуте
            // newValue - это выбранное значение второго уровня
        },
    },
    data() {
        return {
            singleSelectedValue: null,
            relatedGroupsSelectedValue: null,
            selectedSubgroupValue: null,
            baseConfig: {
                typeInput:"underlined",
                label: "input:",
                valueKey: "key",              // json key used to define the value
                labelKey: "keyNLS",           // json key used to define the label displayed
                subGroupKey: "subGroup",      // json key used to define the nested levels of data (used only in the 'second step', ignore it for now)
                required: "false",            // if 'yes', the component must has a selected value
                prefix: {
                    show: "true",     // show or the prefix box
                    style: "",        // custom style to apply on the prefix box
                    text: "",         // prefix text shown
                    minWidth: "90px", // minimum size of the prefix area
                    width: "",        // width of the prefix label. Can be empty, if it is there aren't width limits//   if the prefix the is longer than the width, it have to wrap to a new line
                    align: "left"     // where align the text in the prefix. Possible values are: right | left | center | justify
                },
                placeholder: "",              // the text that appears inside the select/combobox before the user type somethings
                width: "200px",               // total width of the component (including the prefix). It has priority on any other width definition
                initWithFirstValue: "true",   // if false, the component have not a default value selected, otherwise the first value is selected by default
                class: ""                     // the css classes to add to the component
            },
            singleSelectData: [

                {
                    key: "M",           // real value
                    keyNLS: "Metal",    // label displayed
                },
                {
                    key: "P",
                    keyNLS: "Plastic"
                },
                {
                    key: "C",
                    keyNLS: "Composite"
                }

            ],
            relatedGroups:[ // first level
                {
                    key: "01",                  // real value
                    keyNLS: "CILINDRIC PUMP",   // label displayed
                    subGroup:                   // sub related key-values couples
                        [
                            { key: "1", keyNLS: "Type 1" },
                            { key: "2", keyNLS: "Type 2" },
                            { key: "3", keyNLS: "Type 3" },
                            { key: "4", keyNLS: "Type 4" }
                        ]
                },
                {
                    key: "02",
                    keyNLS: "JUNCTION",
                    config: {
                        type: "select",
                        prefix: {
                            text: "Material:"
                        }
                    },
                    subGroup:
                        [ // second level
                            { key: "0", keyNLS: "(Generic)" },
                            { key: "1", keyNLS: "Adapters", subGroup:
                                    [ // third level
                                        { key: "M", keyNLS: "Metal" },
                                        { key: "P", keyNLS: "Plastic" },
                                        { key: "C", keyNLS: "Composite" }
                                    ]
                            },
                            { key: "2", keyNLS: "Elbow" }
                        ]
                },
                {
                    key: "03",
                    keyNLS: "VALVE",
                    subGroup:
                        [
                            { key: "1", keyNLS: "1/2\"" },
                            { key: "2", keyNLS: "3/4\"" },
                            { key: "3", keyNLS: "1\"" },
                            { key: "4", keyNLS: "1 1/2\"" },
                            { key: "5", keyNLS: "2\"" },
                            { key: "8", keyNLS: "TABLED" },
                            { key: "9", keyNLS: "ACCESSORIES" }
                        ]
                },
                {
                    key: "10",
                    keyNLS: "ELECTRICAL RESISTOR",
                    subGroup:
                        [
                            { key: "0", keyNLS: "(Generico)" }
                        ]
                },
                {
                    key: "11",
                    keyNLS: "Non-Return valve",
                    subGroup:
                        [
                            { key: "1", keyNLS: "1/2\"" },
                            { key: "2", keyNLS: "3/4\"" },
                            { key: "3", keyNLS: "Others" }
                        ]
                },
                {
                    key: "12",
                    keyNLS: "Shieldings",
                    subGroup:
                        [
                            { key: "0", keyNLS: "(Generico)" }
                        ]
                }
            ],
        };
    },
};
</script>

<style scoped>
/* Стили для этой страницы (если необходимо) */
</style>
