<template>
    <form action="" @submit.prevent="addNewItem">
        <input type="text" name="" v-model="text" id="" placeholder="e.g. make a blog video">

        <p class="pick-up">Pick a category</p>
        <div class="categories">
            <div class="category">
                <label for="business">
                <input type="radio" name="category" id="business" v-model="category" value="Business">
                <br>
                    <b>Business</b>
                </label>
            </div>
            <div class="category">
                <input type="radio" name="category" id="personal" v-model="category" value="Personal">
                <br>
                <label for="personal">
                    <b>Personel</b>
                </label>
            </div>
        </div>

        <button type="submit">Add TODO</button>
    </form>
</template>

<script setup>
    import { ref } from 'vue';
    import { useToast } from 'vue-toastification';

    const emits = defineEmits(['addToDoItem'])

    const toaster = useToast();
    const text = ref('');
    const category = ref('');
    const todoItem = {};

    const addNewItem = (e) => {
        if (!text.value || !category.value) {
            toaster.error('Both fields are required')
            return;
        }

        todoItem.text = text.value;
        todoItem.category = category.value;

        emits('addToDoItem', todoItem)

        text.value = '';
        category.value = '';
    }
</script>


<style scoped>
    form input[type='text'] {
        background-color: #FEFEFE;
        border: 0;
        outline: 0;
        width: 100%;
        font-size: 18px;
        padding: 10px;
        border-radius: 3px;
        margin: 10px 0 10px 0;
    }

    .pick-up {
        margin-top: 10px;
    }

    .categories {
        display: flex;
        justify-content: space-between;
    }

    .categories .category {
        text-align: center;
        width: 48%;
        background-color: #FEFEFE;
        margin: 10px 0;
        padding: 25px 0;
        border-radius: 3px;
    }

    .category input {
        border: 2px solid black;
    }

    form > input {
        background-color: #E741A2;
        width: 100%;
        padding: 15px 0;
        text-align: center;
        border-radius: 3px;
        color: black;
        border: none;
        text-align: left;
    }

    form > button {
        background-color: #E741A2;
        width: 100%;
        padding: 15px 0;
        text-align: center;
        border-radius: 3px;
        color: white;
        border: none;
        text-align: center;
        font-weight: 700;
    }
</style>