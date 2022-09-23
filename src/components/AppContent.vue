<template>
    <div class="App-Content">
        <div class="Content-Top">
            <content-controls 
                :search-input="searchInput"
                @on-search="inputSearch"
            />
            <content-form 
                :is-show-form="isShowForm"
                :todo-input="todoInput"
                :todo-selected="todoSelected"
                @on-toggle="toggleHandler"
                @on-input="inputHandler"
                @on-store="storeHandler"
                @on-update="updateHandler"
            />
        </div>
        <div class="Content-Bottom">
            <content-todos 
                :todos="todosFiltered"
                @on-del="delHandler"
                @on-edit="editHandler"
            />
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import ContentControls from './ContentControls.vue';
import ContentForm from './ContentForm.vue';
import ContentTodos from './ContentTodos.vue';
import { v4 as uuidv4 } from 'uuid';

// State
const isShowForm = ref(false);
const todoInput = ref('');
const todoSelected = ref(null);
const searchInput = ref('');
const todos = ref([
    {
        id: uuidv4(),
        title: 'đi chơi'
    },
    {
        id: uuidv4(),
        title: 'du lịch'
    },
    {
        id: uuidv4(),
        title: 'khách sạn'
    },
    {
        id: uuidv4(),
        title: 'nghỉ ngơi'
    },
]);

const toggleHandler = () => {
    isShowForm.value = !isShowForm.value;
}

const inputHandler = (value) => {
    todoInput.value = value;
}

const storeHandler = () => {
    if(todoInput.value.trim().length) {
        const newValue = {
            id: uuidv4(),
            title: todoInput.value
        }
        todos.value.push(newValue);
        todoInput.value = '';
        isShowForm.value = false;
    } else {
        alert('Vui lòng nhập Input')
    }
}

const delHandler = (id) => {
    const todoIndex = todos.value.findIndex(todo => todo.id === id)
    if(todoIndex >= 0) {
        todos.value.splice(todoIndex, 1);
    } else {
        alert('this todo is not define')
    }
}

const editHandler = (id) => {
    const todoIndex = todos.value.findIndex(todo => todo.id === id)
    if(todoIndex >= 0) {
        isShowForm.value = true;
        todoSelected.value = todos.value[todoIndex];
        todoInput.value = todoSelected.value.title;
    } else {
        alert('this todo is not define')
    }
}

const updateHandler = () => {
    if(todoInput.value.trim().length) {
        const todoIndex = todos.value.findIndex(todo => todo.id === todoSelected.value.id)
        todos.value[todoIndex] = {
            ...todos.value[todoIndex],
            title: todoInput.value
        }
        todoInput.value = '';
        todoSelected.value = null;
        isShowForm.value = false;
    } else {
        alert('Vui lòng nhập nội dung update')
    }
}

const inputSearch = (value) => {
    searchInput.value = value;
}
const todosFiltered = computed( () => {
    const todoCopped = [...todos.value];
    const todoSearched = todoCopped.filter(todo => {
        const title  = todo.title.toLowerCase();
        const search = searchInput.value.toLowerCase();
        
        return title.includes(search);
    });
    return todoSearched;
})

// // const InputSearchHandler = () => {
// //     const todoCopped = [...todos.value];
//     const todoSearched = todoCopped.filter(todo => {
//         const title  = todo.title.toLowerCase();
//         const search = searchInput.value.toLowerCase();
        
//         return title.includes(search);
//     });
//     todos.value = todoSearched;
// // }
</script>
<style>
.Content-Top {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 10px;
}
</style>