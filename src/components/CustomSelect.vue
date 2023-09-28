<template>
    <div class="input__box">
        <label v-if="config.prefix.show" :style="config.prefix.style">

        </label>
        <v-select
            :items="selectData.map(item => item[config?.labelKey])"
            :placeholder="config?.placeholder"
            v-model="selectedValue"
            :label="config.label "
            :variant="config.typeInput"
            :item-value="config.valueKey"
            :item-text="config.labelKey"
            @change="handleChange"
        />



    </div>
</template>

<script>

export default {
    props: {
        config: Object,
        selectData: Array,
        value: Object, // Принимаем объект в качестве prop
    },
    data() {
        return {
            selectedValue: null,
            selectedSubgroup: null, // Добавляем data для хранения выбранного объекта
        };
    },
    methods: {

        handleChange(newValue) {
            console.log(newValue)

        },
        handleSubgroupChange(newValue) {

        },
    },
};
</script>

<style scoped>
.input__box{
    width: 50%;
    margin: 0 auto;
}

</style>
