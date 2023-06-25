<script>
import axios from 'axios';

export default {
    data() {
        return {
            categories: [],
            stats: []
        }
    },

    mounted() {
        this.loadCategories()
        this.loadDate()
    },

    methods: {
        async loadDate() {
            let response = await axios.get('/stats');
            this.stats = response.data;
        },

        async loadCategories() {
            let response = await axios.get('/categories/all');
            this.categories = response.data;
        },
    }
}
</script>


<template>
    <div class="create-page">
        <h3 class="mb-5">Сводка</h3>
        <div class="categories-container my-5">
            <label v-for="(item, index) in categories" class="category">
                <div class="category-info">
                    <img :src="'src/assets/' + item.value + '.svg'">
                    {{ item.title }}
                </div>
            </label>
        </div>
    </div>
</template>


<style>
.create-page h3 {
    text-align: center;
}

.create-page .category {
    display: flex;
    flex-direction: column;
    width: 20%;
    align-items: center;
    justify-content: center;
}

.category {
    position: relative;
}

.category img {
    width: 60%;
}

.category-input {
    display: none;
}


.category-info {
    display: flex;
    flex-direction: column;
    gap: 10px;
    align-items: center;
    justify-content: center;
    padding: 10px;

    transition: scale 300ms;
}

/* Выбранная радиокнопка */
.category .category-input:checked~.category-info {
    scale: 1.4;
}

.categories-container {
    display: flex;
}

.note-container {
    display: flex;
    gap: 10px;
    justify-content: space-between;
}

.note-container .note-input-container {
    flex: 1;
}
</style>