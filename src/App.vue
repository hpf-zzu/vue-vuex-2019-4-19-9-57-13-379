<template>
    <div id="app">
        <h2>
            Vue To Do List
            Simple Todo List with adding and filter by diff status.
        </h2>
        <CreateForm @addHandle = "addInput" @addHandleChange = "addChange">
        </CreateForm>
        <!-- <div id = "addTodoForm">
            <input type = "text" v-model="inputingText">
            <button @click="handleAdd">Add</button>

        </div> -->

        <div id = "list">
            <ul>
                <li v-for="(item,index) in filteredTodoList" :key="index">
                    <input type = "checkbox" @click= "selectItem(item)" v-model="item.select">
                    {{item.content}}

                </li>
            </ul>
        </div>
         <div id = "filter">
            <button @click="handleStatusUpdate('active')">Active</button>
            <button @click="handleStatusUpdate('completed')">Completed</button>
            <button @click="handleStatusUpdate('all')">All</button>
        </div>
    </div>
</template>

 <script>
 import CreateForm from "./components/CreateForm.vue";
// import { METHODS } from 'http';
// import func from '../vue-temp/vue-editor-bridge';
// import { resolve } from 'dns';
   
    export default {
        name: 'app',
        components: {
           CreateForm
        },
        data: function () {
            return {
                /**
                 * 定义了 todo item 中属性为 {content:'吃饭',status:'active'}
                 * 定义了 todo 的两种状态 completed、active，默认为 active
                 */
                todoList: [
                    {content: "吃饭",  status: 'completed'},
                    {content: "写作业", status: 'active'},
                    {content: "打豆豆", status: 'active'}
                
                ],
                currentFilter: "all",
                inputingText: "",
                flag: true
                
            }
        },
        computed:{
            filteredTodoList: function(){
                let filterList = [];
                for(let index = 0; index < this.todoList.length; index ++){
                    const element = this.todoList[index];
                    if(element.status === this.currentFilter || this.currentFilter == 'all'){
                        filterList.push(element);
                    }
                }

                //return this.todoList.filter(element => element.status === this.currentFilter);
               return filterList;
            }

        },
        methods:{
            addInput: function(inputingText){
                this.todoList.push(
                    {content: inputingText,
                     status: "active"
                    }
                );

            },
            addChange: function(param){
                this.inputingText = param;
            },

            handleStatusUpdate:function(status){
                this.currentFilter = status;

            },
            selectItem(item){
                item.select = !item.item;
                if(item.select){
                    item.status = "completed";

                }else{
                    item.status = "active";

                }

            }

        }


    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    .items {
        list-style: none;
        text-align: left;
        line-height: 30px;
    }

    .items li.completed {
        text-decoration: line-through;
    }

    .filter a {
        margin: 0 10px;
        line-height: 30px;
    }

    .filter a.active {
        color: #f60;
        border: 1px solid #ccc;
        border-radius: 2px;
        padding: 3px;
        cursor: pointer;
    }
</style>
