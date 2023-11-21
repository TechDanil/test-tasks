<template>
    <div class="table-container">
        <table>
            <thead>
                <tr>
                    <th @click="sortBy('number')">Номер<img v-if="sortKey === 'number'"
                            :src="sortOrder === 'asc' ? arrowUp : arrowDown" alt="Sort" /></th>
                    <th @click="sortBy('developer')">Девелопер<img v-if="sortKey === 'developer'"
                            :src="sortOrder === 'asc' ? arrowUp : arrowDown" alt="Sort" /></th>
                    <th @click="sortBy('deadline')">Срок<img v-if="sortKey === 'deadline'"
                            :src="sortOrder === 'asc' ? arrowUp : arrowDown" alt="Sort" /></th>
                    <th @click="sortBy('type')">Тип<img v-if="sortKey === 'type'"
                            :src="sortOrder === 'asc' ? arrowUp : arrowDown" alt="Sort" /></th>
                    <th @click="sortBy('floor')">Этаж<img v-if="sortKey === 'floor'"
                            :src="sortOrder === 'asc' ? arrowUp : arrowDown" alt="Sort" /></th>
                    <th @click="sortBy('square')">Площадь<img v-if="sortKey === 'square'"
                            :src="sortOrder === 'asc' ? arrowUp : arrowDown" alt="Sort" /></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in sortedData" :key="item.id">
                    <td>{{ item.number }}</td>
                    <td>{{ item.developer }}</td>
                    <td>{{ formatDate(item.deadline) }}</td>
                    <td>{{ item.type }}</td>
                    <td>{{ item.floor }}</td>
                    <td>{{ item.square }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'CustomTable',
    data() {
        return {
            data: [
                {
                    id: 1,
                    number: 421,
                    developer: 'PRINZIP',
                    deadline: '2005-08-09T18:31:42',
                    type: 'Студия',
                    floor: 2,
                    square: 100.3
                },
                {
                    id: 2,
                    number: 73,
                    developer: 'Брусника',
                    deadline: '2005-08-09T18:31:42',
                    type: '2-к',
                    floor: 2,
                    square: 10.3
                },
                {
                    id: 3,
                    number: 122,
                    developer: 'TEN',
                    deadline: '2005-08-09T18:31:42',
                    type: '3-к',
                    floor: 2,
                    square: 103
                },
                {
                    id: 4,
                    number: 1,
                    developer: 'PRINZIP',
                    deadline: '2005-08-09T18:31:42',
                    type: 'Студия',
                    floor: 2,
                    square: 100.3
                },
                {
                    id: 5,
                    number: 72,
                    developer: 'Брусника',
                    deadline: '2005-08-09T18:31:42',
                    type: '2-к',
                    floor: 2,
                    square: 10.3
                },
                {
                    id: 6,
                    number: 23,
                    developer: 'TEN',
                    deadline: '2005-08-09T18:31:42',
                    type: '3-к',
                    floor: 2,
                    square: 103
                },
                {
                    id: 7,
                    number: 5,
                    developer: 'PRINZIP',
                    deadline: '2005-08-09T18:31:42',
                    type: 'Студия',
                    floor: 2,
                    square: 100.3
                },
                {
                    id: 8,
                    number: 2,
                    developer: 'Брусника',
                    deadline: '2005-08-09T18:31:42',
                    type: '2-к',
                    floor: 2,
                    square: 10.3
                },
                {
                    id: 9,
                    number: 97,
                    developer: 'TEN',
                    deadline: '2005-08-09T18:31:42',
                    type: '3-к',
                    floor: 2,
                    square: 103
                },
                {
                    id: 10,
                    number: 34,
                    developer: 'PRINZIP',
                    deadline: '2005-08-09T18:31:42',
                    type: 'Студия',
                    floor: 2,
                    square: 100.3
                },
                {
                    id: 11,
                    number: 1,
                    developer: 'Брусника',
                    deadline: '2005-08-09T18:31:42',
                    type: '2-к',
                    floor: 2,
                    square: 10.3
                },
                {
                    id: 12,
                    number: 88,
                    developer: 'TEN',
                    deadline: '2005-08-09T18:31:42',
                    type: '3-к',
                    floor: 2,
                    square: 103
                },

            ],
            sortKey: '',
            sortOrder: 'asc',
            arrowUp: require('@/assets/arrowSort.svg'),
            arrowDown: require('@/assets/arrowSort.svg'),
        };
    },
    computed: {
        sortedData() {
            if (!this.sortKey) return this.data;

            return this.data.slice().sort((a, b) => {
                const valueX = a[this.sortKey];
                const valueY = b[this.sortKey];

                if (typeof valueX === 'number' && typeof valueY === 'number') {
                    return this.sortOrder === 'asc' ? valueX - valueY : valueY - valueX;
                } else if (typeof valueX === 'string' && typeof valueY === 'string') {
                    return this.sortOrder === 'asc' ? valueX.localeCompare(valueY) : valueY.localeCompare(valueX);
                } else if (valueX instanceof Date && valueY instanceof Date) {
                    return this.sortOrder === 'asc' ? valueX - valueY : valueY - valueX;
                }

                return 0;
            });
        }
    },
    methods: {
        sortBy(key) {
            if (this.sortKey === key) {
                this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc';
            } else {
                this.sortKey = key;
                this.sortOrder = 'asc';
            }
        },
        formatDate(dateString) {
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            return new Date(dateString).toLocaleDateString('ru-RU', options);
        }
    }
}
</script>

<style scoped>
    .table-container {
        margin-top: 100px;
        max-height: 600px;
        overflow-y: scroll;
    }

    table {
        width: 100%;
        border-collapse: collapse;
    }
    
    thead {
        position: sticky;
        top: 0;
    }

    th,
    td {
        border: 1px solid #ddd;
        padding: 8px;
        text-align: left;
    }

    th {
        cursor: pointer;
        background-color: #F968bf;
        color: #fff;
    }

    th img {
        margin-left: 5px;
    }

    th img[src$=".svg"] {
        fill: #29277d;
    }
</style>