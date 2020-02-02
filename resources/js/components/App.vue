<template>
    <div class='app-component'>
        <table class='table'>
            <thead>
                <th>Task Title</th>
                <th>Priority</th>
                <th>Action</th>
            </thead>
            <tbody>
                <task-component></task-component>
               <tr>
                   <td>
                       <input type="text" id="task" class="form-control">
                   </td>
                   <td>
                       <select id="select" class="form-control">
                           <option value="">Low</option>
                           <option value="">Medium</option>
                           <option value="">High</option>
                       </select>
                   </td>
                   <td>
                       <button class="btn btn-primary">ADD</button>
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
            message: 'hello from here...',
        };
    }
}
</script>>

<style>

</style>