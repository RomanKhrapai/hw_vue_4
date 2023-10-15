
<template>
    <div class="lists-box">
        <div class="column">
            <h3>список у списку</h3>
            <ul>
                <li v-for="item, i in zooArray" :key='i'>
                    <h4>{{ (i + 1) }}. {{ item.species }}</h4>
                    <ul class="animal">
                        <li v-for="animal, j in item.subspecies" :key='j'>
                            {{ (i + 1) }}.{{ (j + 1) }}. {{ animal.name }} - {{ animal.quantity }}шт.
                        </li>
                    </ul>
                </li>
            </ul>

        </div>
        <div class="column">
            <h3>список з пагінацією</h3>
            <ul>
                <li class="item" v-for="contact in getItemsContact" :key='contact.id'>
                    {{ contact.name }}<br> {{ contact.phone }}


                </li>
            </ul>

            <div class="control" v-if="contacts.length > quantity">

                <button :disabled="page === 1" class="btn" @click="prevPage" :class="{ 'night': !isLight }">&#60;</button>
                <input type="number" v-model="quantity" min="1" max="50" :class="{ 'night': !isLight }" />
                <button :disabled="lastPage" class=" btn" @click="nextPage" :class="{ 'night': !isLight }">&#62;</button>
            </div>

        </div>
        <div class="column">
            <input type="date" v-model="date" :class="{ 'night': !isLight }" />
            <h3>список з фільтром за датою</h3>
            <ul>
                <template v-for="contact in contacts" :key="contact.id">
                    <li class="item" v-if="conditionFilterDate(contact.createdAt)">
                        {{ contact.name }}<br> {{ formatDate(contact.createdAt) }}
                    </li>
                </template>
            </ul>
        </div>

    </div>
</template>

<script>
import axiosInstance from "../../services/axios.js"

export default {
    props: ["isLight"],

    data() {
        return {
            date: '2023-10-14',
            zooArray: [
                {
                    species: 'Ссавці',
                    subspecies: [
                        { name: 'Лев', quantity: 2 },
                        { name: 'Слон', quantity: 3 },
                        { name: 'Тигр', quantity: 1 },
                        { name: 'Ведмідь', quantity: 2 },
                        { name: 'Верблюд', quantity: 0 },

                    ]
                },
                {
                    species: 'Птахи',
                    subspecies: [
                        { name: 'Сокіл', quantity: 0 },
                        { name: 'Голуб', quantity: 1 },
                        { name: 'Качка', quantity: 2 },
                        { name: 'Страус', quantity: 8 },
                        { name: 'Пінгвін', quantity: 4 },

                    ]
                },
                {
                    species: 'Рептилії',
                    subspecies: [
                        { name: 'Крокодил', quantity: 0 },
                        { name: 'Ящірка', quantity: 3 },
                        { name: 'Гадюка', quantity: 1 },
                        { name: 'Черепаха', quantity: 2 },
                        { name: 'Алігатор', quantity: 0 },

                    ]
                },

            ],
            page: 1,
            quantity: 10,
            contacts: []
        }

    },
    methods: {
        getContacts() {
            axiosInstance.get('/contacts').then(res => {
                this.contacts = res.data
            }).catch(error => {
                console.log(error)
            })
        },
        nextPage() {
            this.page++
        },
        prevPage() {
            this.page--
        },
        formatDate(dateOld) {
            const date = new Date(dateOld);
            const year = date.getFullYear();
            const month = date.getMonth() + 1;
            const day = date.getDate();

            return `Дата: ${day}-${month}-${year}`
        },
        conditionFilterDate(contactDate) {
            const date = new Date(contactDate);
            const year = date.getFullYear();
            const month = date.getMonth() + 1;
            const day = date.getDate();
            return `${year}-${month}-${day}` === this.date
        }

    },
    computed: {
        getItemsContact() {
            const finish = this.page * this.quantity;
            const start = finish - this.quantity;
            return this.contacts.slice(start,
                this.contacts.length <= finish ? this.contacts.length - 1 : finish);
        },
        lastPage() {
            return this.contacts.length <= this.page * this.quantity
        }
    },
    mounted() {
        this.getContacts()
    }
}

</script>
<style scoped>
.control {
    display: flex;
    flex-wrap: nowrap;
}

.lists-box {
    display: flex;
}

.column {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
}

h4,
h3 {
    margin: 5px;
}

ul {
    padding: 0;
    margin: 0;
    list-style: none;
    overflow-y: auto;
}

.night {
    background-color: rgb(8, 56, 8);
    color: #ffffff;
    border: 1px solid #fff;
}

.animal {
    padding-left: 15px;
}

.item:nth-child(even) {
    background-color: rgba(0, 0, 255, 0.321);
}
</style>