<template>
    <select v-model="modelValue" @change="changeOption">
        <option disabled value="">
            Виберіть фільтр
        </option>
        <option 
            v-for="option in options"
            :key="option.value"
            :value="option.value"
        >
            {{option.name}}
        </option>
    </select>
</template>

<script>
export default {
    name: "my-select",

    props: {
        modelValue: {
            type: String
        },

        options: {
            type: Array,
            deafult: () => []
        }
    },

    methods: {
        changeOption(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style>
select {
    align-self: flex-end;
    background-color: white;
    color: teal;
    border: 1px solid teal;
    padding: 10px;
    cursor: pointer;
}
</style>