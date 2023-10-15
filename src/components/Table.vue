<template>
    <div>
        <label :class="{ 'night': !isLight }"><input type="range" v-model="columns" min="1" max="11" /> рядок </label>
        <label :class="{ 'night': !isLight }"><input type="range" v-model="rows" min="1" max="11" /> стовбець </label>

        <table :class="{ 'night': !isLight }">
            <tr v-for="row in +rows">
                <td :class="{ 'night': !isLight }" v-for="colunm in +columns">{{ row + "-" + colunm }}</td>

            </tr>

        </table>

    </div>
</template>

<script>

export default {
    props: ["isLight"],

    data() {
        return {
            rows: 1,
            columns: 1,
        }
    },
    computed: {
        getrows() {
            return
        }
    }
}

</script>
<style scoped>
.night {
    background-color: rgb(8, 56, 8);
    color: #ffffff;
    border: 1px solid #fff;
}

table,
td {
    border: 1px solid #1d1c1c;
}
</style>