<template>
    <div class="notes">
        <!-- <ul>
            <li v-for="task in tasks">
                <h3>{{ task.order }}</h3>
                <p>Priority: {{ task.priority }}</p>
                <p>Date: {{ task.date }}</p>
                <p>Status: 
                    <span v-if="task.status">Completed</span>
                    <span v-else>Not Completed</span>
                </p>
            </li>
        </ul> -->
        <div class="d-flex justify-content-center">
            <h1>Tasks Manager</h1>
        </div>

        <hr>

        <h2>New Task</h2>

        <input type="text" name="" v-model="textNewTask" placeholder="New Task" v-on:keyup.enter="newTask">
        <button value="Create" v-on:click="newTask">Create</button>

        <p>Tasks number: {{ tasks.length }}</p>
        <p>Tasks to do: {{ taskToDo() }}</p>

        <h2>Show Tasks</h2>
        <input type="checkbox" id="completed" value="Completed" v-model="checkedStatus">
        <label for="jack">Completed Tasks</label>
        <br>
        <input type="checkbox" id="incompleted" value="Incompleted" v-model="checkedStatus"> 
        <label for="john">Incompleted Tasks</label>
        
        <ul>
            <li v-for="auxTask in checkedTask">
                <h3>{{ auxTask.order }}</h3>
                <p>Priority: {{ auxTask.priority }}</p>
                <p>Date: {{ auxTask.date }}</p>
                <p>Status: 
                    <span v-if="auxTask.status">Completed</span>
                    <span v-else>Not Completed</span>
                </p>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'Notes',
        props: [],
        data: function() {
            return{
                tasks: [
                    {
                        order: "Clean the dishes",
                        priority: Math.floor(Math.random() * (4 - 1)) + 1,
                        date: new Date().toLocaleString(),
                        status: false
                    },
                    {
                        order: "Take the dog out",
                        priority: Math.floor(Math.random() * (4 - 1)) + 1,
                        date: new Date().toLocaleString(),
                        status: true
                    }
                ],
                textNewTask: "",
                checkedStatus: [],
                auxTasks: [],
                show: true
            }
        },
        methods: {
            newTask: function(event){
                var order = this.textNewTask;
                var date = new Date().toLocaleString();
                var priority = Math.floor(Math.random() * (4 - 1)) + 1;
                var status = false;
                this.tasks.push({order, date, priority, status});
            },
            taskToDo: function(){
                var count = 0;
                for(let i=0; i<this.tasks.length; i++){
                    if(this.tasks[i].status == false){  
                        count++;
                    }
                }
                return count;
            }
        },
        computed: {
            checkedTask: function(){
                this.auxTasks = [];
                for(let j=0; j<this.checkedStatus.length; j++){
                    if(this.checkedStatus[j] == "Completed"){
                        for(let i=0; i<this.tasks.length; i++){
                            if(this.tasks[i].status == true){
                                this.auxTasks.push(this.tasks[i]);
                            }
                        }
                    }
                    if(this.checkedStatus[j] == "Incompleted"){
                        for(let i=0; i<this.tasks.length; i++){
                            if(this.tasks[i].status == false){
                                this.auxTasks.push(this.tasks[i]);
                            }
                        }
                    }
                }
                return this.auxTasks;
            }
        }
    }
</script>

<style>
    #presentation{
        text-align: center;
    }
</style>
