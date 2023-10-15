
<template>
    <ul>
        <li class="random-item" v-for="item in styles" :key="item.id" :style="item.style">
            text
        </li>
    </ul>
</template>

<script>
import CustomButton from './CustomButton.vue'

export default {
    components: {
        CustomButton
    },
    data() {
        return {
            dateArray: [],
            styles: []
        }
    },
    methods: {
        randomNum(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        },
        createStyles() {
            const r = this.randomNum(0, 255)
            const g = this.randomNum(0, 255)
            const b = this.randomNum(0, 255)
            const brightness = (r * 299 + g * 587 + b * 114) / 1000;

            return {
                color: brightness > 128 ? "#000" : "#FFF",
                backgroundColor: "#" + this.makeTwoDigits(r) + this.makeTwoDigits(g) + this.makeTwoDigits(b),
                fontSize: this.randomNum(5, 40) + 'px'
            }
        },
        makeTwoDigits(num) {
            return (num < 16) ? "0" + num.toString(16) : num.toString(16);
        },
    },
    created() {
        for (let i = 0; i <= this.randomNum(2, 30); i++) {
            this.styles.push({ id: i, style: this.createStyles() })
        }
    }
}

</script>
<style scoped>
ul {
    list-style: none;
    display: flex;
    border: solid #333;
    padding: 3px;
    flex-wrap: wrap;
}

.random-item {
    height: 40px;
    min-width: 40px;
    padding: 0 3px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex: auto
}
</style>