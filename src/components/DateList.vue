
<template>
    <div>
        <CustomButton :class="{ 'night-btn': !isLight }" @click="saveDate">
            Додати час кліку
        </CustomButton>
        <ul>
            <li v-for="item in dateArray">
                {{ item }}
            </li>
        </ul>
    </div>
</template>

<script>
import CustomButton from './CustomButton.vue'

export default {
    props: ["isLight"],
    components: {
        CustomButton
    },
    data() {
        return {
            dateArray: []
        }
    },
    methods: {
        saveDate() {
            this.dateArray.push(new Date())
        },
    }
}

</script>
<style scoped>
ul {
    max-height: 100px;
    overflow-y: auto;
}

.night-btn {
    background-color: rgb(8, 56, 8);
    color: #ffffff;
    border: 1px solid #fff;
}
</style>