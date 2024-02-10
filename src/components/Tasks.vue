<template>
    <div class="tasksContainer">
        <Task :key="task.id" v-for="task in tasks" :task="task" @delete-task="$emit('delete-task', task.id)"
            @checkbox-updated="updateTaskCheckbox" @edit-task="$emit('edit-task', task.id, task.taskValue)" />
    </div>
</template>


<script>

import Task from "./Task.vue"
export default {
    name: 'Tasks',
    props: {
        tasks: Array
    },
    components: {
        Task
    },
    methods: {
        updateTaskCheckbox({ taskId, isChecked }) {
            console.log(isChecked);
            const updatedTasks = this.tasks.map(task => {
                if (task.id === taskId) {
                    return { ...task, checked: isChecked };
                }
                return task;
            });
            // console.log(updatedTasks);
            this.$emit('tasks-updated', updatedTasks);
        }
    }
}
</script>





<style>
.tasksContainer {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}
</style>