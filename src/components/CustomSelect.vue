<template>
    <div class="input__box">
        <label v-if="!config.prefix.show" :style="config.prefix.style">{{ config.prefix.text }}</label>
        <v-select
            :items="selectData"
            :item-text="config.labelKey"
            :item-value="config.key"
            :placeholder="config?.placeholder"
            v-model="selectedValue"
            :label="config.label"
            :variant="config.typeInput"
            @update:modelValue="handleChange"
        />
        <p>Выбранное значение: {{ selectedValue ? selectedValue[config.labelKey] : '' }}</p>
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
        handleChange(newValue) {
            console.log(newValue)
            this.selectedValue = newValue;
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
