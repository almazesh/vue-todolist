<template>
    <div class="container">
        <h2 class="text-center mt-5">My Vue Todo App</h2>
        
        <form class="d-flex mt-5">
            <input v-model="task" type="text" placeholder="Enter task" class="form-control">
            <div @click="submitTask" class="btn btn-warning rounded">Submit</div>
        </form>


        <div class="d-flex justify-content-center">
            <table class="table table-bordered mt-5 w-75">
                <thead>
                    <tr>
                    <th scope="col" class="text-center">Task</th>
                    <th scope="col" class="text-center">Status</th>
                    <th scope="col" class="text-center">#</th>
                    <th scope="col" class="text-center">#</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(todo) of tasks" :key="todo.id">
                        <td>{{todo.name}}</td>
                        <td class="text-center" @click="changeStatus(todo.id)">{{todo.status}}</td>
                        <td class="text-center text-primary" @click="editedTask(todo.id)">Edit</td>
                        <td class="text-center text-danger" @click="deleteTask(todo.id)">Delete</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>




<script>
    export default {
        task:'',
        statuses:['to-do' , 'in-progress' , 'successed'],
        methods:{
            submitTask(){
                if(this.task.length === 0) return;

                this.tasks.push({
                    name:this.task,
                    status:'to-do'
                })

                this.task = '';
            },



            deleteTask(index){
                this.tasks = this.tasks.filter(item => item.id !== index)
            },


            editedTask(index){
                this.tasks = this.tasks.map(item => {
                    if(item.id === index){
                        return {
                            ...item ,
                            name:window.prompt('New task?'  , item.name)
                        }
                    }else{
                        return item
                    }
                })
            },

            changeStatus(index){
                let newIndex = this.statuses.indexOf(this.tasks[index].status)
                if(++index > 2) newIndex = 0;
                this.tasks[index].status = this.statuses[newIndex]
            },     
        }, 

       

        data(){
            return{
                tasks:[
                    {
                        id:1,
                        name:'Work over the goal',
                        status:'to-do'
                    },
                    {
                        id:2,
                        name:"Get the NYC",
                        status:"in-progress"
                    },
                    
                ]
            }
        }
    }
</script>



<style scoped>
    table{
        transition: 1s;
    }

    td{
        cursor: pointer;
    }
</style>