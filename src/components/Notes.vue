<template>
    <div class="notes">

        <!-- TASKS LAYOUT ORIGNAL -->
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

        <!-- TITLE -->
        <section class="container">
            <div class="row">
                <div class="col" style="text-align:center;">
                    <h1>Tasks Manager</h1>
                </div>
            </div>
        </section>
        
        <div class="dropdown-divider bg-secondary"></div>
        
        <!-- START UP LAYOUT AND INFO -->
        <section class="container">
            <!-- NEW TASK -->
            <div class="row">
                <div class="col-md-9 col-12">
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text bg-secondary text-white" id="inputGroup-sizing-default">New Task</span>
                        </div>
                        <input type="text" class="form-control" aria-label="Default" aria-describedby="inputGroup-sizing-default" placeholder="What do you want to do?" v-on:keyup.enter="newTask" v-model="textNewTask">
                    </div>
                    <!-- <input type="text" name="" v-model="textNewTask" placeholder="Insert a new tasks" v-on:keyup.enter="newTask"> -->
                </div> 
                <div class="col-md-2 offset-md-1 col-12">
                    <button type="button" class="btn btn-secondary btn-block" v-on:click="newTask">Create</button>
                    <br>
                </div>        
            </div>
            
            <!-- TASKS INFO -->
            <div class="row  justify-content-md-start">
                <div class="col-sm-12 col-md-auto">
                    <small>
                        <span>{{ tasks.length }} pending tasks of a total {{ taskToDo() }} | </span>
                        <span class="text-warning"><b>Delete comspanleted tasks</b></span>
                    </small>
                </div>
            </div>
        </section>

        <div class="dropdown-divider bg-secondary"></div>

        <br>

        <div class="row">
            <div class="col-12" style="text-align:center;">
                <h2>Tasks</h2>
            </div>
            <div class="col-12">
                <ul>
                    <li v-for="task in priorityFilter"  style="list-style:none;">
                        <div class="row justify-content-between">
                            <div class="col-auto">
                                <div class="row">
                                    <div class="col-auto">
                                        <span v-if="task.status"><img src="../../public/completed.svg" alt="" height="50px" width="auto" style="float:left;" class="svg"></span>
                                        <span v-else><img src="../../public/incompleted.svg" alt="" height="50px" width="auto" style="float:left;"></span>
                                    </div>
                                    <div class="col-auto">
                                        <div class="row">
                                            <!-- ORDER -->
                                            <!-- VARIABLE {{ task.order }} -->
                                                <!-- <del>{{ task.order }}</del> -->
                                            <div>
                                                <h3 v-if="task.status" class="text-success">{{ task.order }}</h3>
                                                <h3 v-else>{{ task.order }}</h3>
                                            </div>               
                                        </div>
                                        <div class="row">
                                            <small>
                                                <!-- PRIORITY -->
                                                <span>Priority: </span>
                                                
                                                <!-- VARIABLE {{ task.priority }} -->
                                                <span>
                                                    <!-- LOW -->
                                                    <button v-if="task.priority == 'Low'" type="button" class="btn btn-primary btn-sm">Low</button>
                                                    <button v-else type="button" class="btn btn-secondary btn-sm">Low</button>
                                                    <span>&nbsp;</span>

                                                    <!-- <span v-if="task.priority == 'Low'" class="bg-primary text-white" style="padding: 0 2px; border:">Low</span>
                                                    <span v-else class="text-primary"> Low </span> -->

                                                    <!-- MEDIUM -->
                                                    <button v-if="task.priority == 'Medium'" type="button" class="btn btn-warning btn-sm">Medium</button>
                                                    <button v-else type="button" class="btn btn-secondary btn-sm">Medium</button>
                                                    <span>&nbsp;</span>

                                                    <!-- <span v-if="task.priority == 'Medium'" class="bg-warning text-white" style="padding: 0 2px;">Medium</span>
                                                    <span v-else class="text-warning"> Medium </span> -->

                                                    <!-- HIGH -->
                                                    <button v-if="task.priority == 'High'" type="button" class="btn btn-danger btn-sm">High</button>
                                                    <button v-else type="button" class="btn btn-secondary btn-sm">High</button>
                                                    <span>&nbsp;</span>

                                                    <!-- <span v-if="task.priority == 'High'" class="bg-danger text-white" style="padding: 0 2px;">High</span>
                                                    <span v-else class="text-danger"> High </span> -->
                                                </span>
                                                <span> | Date: {{ task.date }} </span>
                                            </small>
                                        </div> 
                                    </div>
                                </div>
                            </div>
                            <div class="col-auto">
                                <div class="row">
                                    <div class="col-auto">
                                        <img src="../../public/delete.svg" alt="" height="50px" width="auto" style="float:left;" class="svg">                                
                                    </div>
                                    <div class="col-1"></div>
                                </div>
                            </div>    
                        </div>                     
                    </li>
                </ul>
            </div>
        </div>








        <!-- NEED LAYOUT, REQUESTED TASKS -->
        <br>

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
                        priority: "Low",
                        date: new Date().toLocaleString(),
                        status: false
                    },
                    {
                        order: "Take the dog out",
                        priority: "High",
                        date: new Date().toLocaleString(),
                        status: true
                    }
                ],
                textNewTask: "",
                checkedStatus: [],
                auxTasks: [],
                priorityTasks: [],
                show: true
            }
        },
        methods: {
            newTask: function(event){
                var order = this.textNewTask;
                var date = new Date().toLocaleString();
                var priority = "Medium";
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
            },
            priorityFilter: function(){
                this.priorityTasks = [];
                for(let i=0; i<this.tasks.length; i++){
                    if(this.tasks[i].priority == "High"){
                        this.priorityTasks.push(this.tasks[i]);
                    }
                }
                for(let i=0; i<this.tasks.length; i++){
                    if(this.tasks[i].priority == "Medium"){
                        this.priorityTasks.push(this.tasks[i]);
                    }
                }
                for(let i=0; i<this.tasks.length; i++){
                    if(this.tasks[i].priority == "Low"){
                        this.priorityTasks.push(this.tasks[i]);
                    }
                }
                return this.priorityTasks;
            }
        }
    }
</script>

<style>
    #presentation{
        text-align: center;
    }
    
    li{
        margin: 20px 0;
    }

    span button{
        width: auto;
        font-size: 10px !important;
    }
</style>