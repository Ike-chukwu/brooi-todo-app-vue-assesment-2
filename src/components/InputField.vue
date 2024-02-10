<template>
    <div class="inputContainer">
        <input v-model="taskValue" type="text" placeholder="Enter your task" class="main-input" />
        <button @click="addTask()" class="addBtn">
            <i class="fas fa-plus"></i>
        </button>
    </div>
</template>


<script>

export default {
    name: 'InputField',
    components: {
    },
    data() {
        return {
            taskValue: '',
        }
    },
    methods: {
        addTask() {

            if (!this.taskValue) {
                return
            }

            const newTask = {
                id: Math.random().toFixed(4),
                taskValue: this.taskValue
            }

            console.log(newTask);
            this.$emit('add-new-task', newTask)
            this.taskValue = ""
        }
    }
}

</script>


<style>
.inputContainer {
    width: 100%;
    background: white;
    color: black;
    display: flex;
    align-items: center;
    height: 40px;
    padding-inline: 1rem;
}


.todo-container .inner-todo-container .inputContainer .main-input {
    padding: .2rem;
    width: 94%;
    height: 100%;
    border: none;
    outline: none;
}

.todo-container .inner-todo-container .inputContainer .addBtn {
    border: none;
    background: #C8ABFD;
    color: white;
    font-weight: bold;
    padding: .4rem .5rem;
    cursor: pointer;
}
</style>