<template>
    <select @change="onChange" v-model="selected" class="form-select mt-5 block w-8/12 border p-3 rounded items-center">
        <option value="0">Select Country</option>
        <option v-for="country in countries" :value="country" :key="country.ID">{{country.Country}}</option>
    </select>

</template>

<script>
export default {
    name: 'CountrySelect',
    props: ['countries'],
    data() {
        return {
            selected: 0
        }
    },
    methods: {
        onChange: function() {
            const country = this.countries.find(item => item.ID === this.selected.ID)
            this.$emit('get-country', country)
        }
    }
}
</script>