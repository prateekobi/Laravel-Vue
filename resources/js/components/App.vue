<template>
    <div class='app-component'>

        <loading :active.sync="isLoading"></loading>


        <table class='table'>
            <thead>
                <th>ID</th>
                <th>Task Title</th>
                <th>Priority</th>
                <th>Action</th>
            </thead>
            <tbody>
                <task-component v-model="task.title" v-for="task in tasks" :key="task.id" :task="task" @delete="remove"></task-component>
                
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
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.css';

export default {
    components: {
        TaskComponent,
        Loading,
    },

    data() {
        return {
            tasks: [],
            task: {title: '', priority: ''},

            // Loading properties
            isLoading: false,
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
            if (this.checkInputs()) {
                this.isLoading = true;
                window.axios.post('/api/tasks', this.task).then(savedTask => {
                this.tasks.push(savedTask.data);

                this.task.title = '';
                this.task.priority = '';
                this.isLoading = false;
            });
            }
          
        },
        checkInputs() {
            if (this.task.title && this.task.priority) {
                return true;
            }
        },
        remove(id) {
            this.isLoading = true;
            window.axios.delete(`/api/tasks/${id}`).then(() => {
                let index = this.tasks.findIndex(task => task.id === id);
                this.tasks.splice(index, 1);
                this.isLoading = false;
            });
        },
    },
    created() {
        this.getTasks();
    }
}
</script>>

<style>

</style>