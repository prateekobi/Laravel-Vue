<template>
    <div class='app-component'>
        <table class='table'>
            <thead>
                <th>ID</th>
                <th>Task Title</th>
                <th>Priority</th>
                <th>Action</th>
            </thead>
            <tbody>
                <task-component v-model="task.title" v-for="task in tasks" :key="task.id" :task="task"></task-component>
                
               <tr>
                   <td>
                       <input v-model="task.title" type="text" id="task" class="form-control">
                   </td>
                   <td>
                       <select v-model="task.priority" id="select" class="form-control">
                           <option>Low</option>
                           <option>Medium</option>
                           <option>High</option>
                       </select>
                   </td>
                   <td>
                       <button @click="store" class="btn btn-primary">ADD</button>
                   </td>
               </tr>
            </tbody>
        </table>
    </div>

</template>

<script>
import TaskComponent from './Task.vue';

export default {
    components: {
        TaskComponent,
    },

    data() {
        return {
            tasks: [],
            task: {title: '', priority: ''},
        };
    },
    methods: {
        getTasks() {
            window.axios.get('/api/tasks').then(({data})=>{
                data.forEach(task => {
                    this.tasks.push(task)
                });
            });
        },
        store() {
            window.axios.post('/api/tasks', this.task).then(savedTask => {
                this.tasks.push(savedTask.data);
            });
        }
    },
    created() {
        this.getTasks();
    }
}
</script>>

<style>

</style>