<template>
    <div class="main-todo">
        <input type="text" class="add-todo" placeholder="what to do?" autofocus v-model="content" @keyup.enter="addTodo">
        <todo-item v-for="(item, index) in filterData" :key="index" :todo="item" @del="handleDeleteItem"></todo-item>
        <todo-info :total="total" @toggleState="handleToggleState" @clearCompleted="handleClear"></todo-info>
    </div>
</template>

<script>
import TodoItem from './coms/TodoItem.vue'
import TodoInfo from './coms/TodoInfo.vue'

let id = 0;
export default {
    name:'MainTodo',
    data(){
        return {
            todoData: [],
            content:'',
            total:0,
            filter:'all',
        }
    },
    methods:{
        addTodo(){
            if(this.content === '') return;

            let today = new Date();
            let currentTime = `${today.getFullYear()}/${today.getMonth()+1}/${today.getDay()}  ${today.getHours()}:${today.getMinutes()}`;

            this.todoData.unshift({
                id: id++,
                content: this.content,
                time: currentTime,
                completed: false
            });


            this.content = '';
        },
        handleDeleteItem(id){
            this.todoData.splice(this.todoData.findIndex(function(item){return item.id ===id}), 1);//用findIndex在this.todoData数组里找到id等于从子组件传过来的id的对象（item）的下标index，然后删除掉一个。
        },
        handleToggleState(state){
            this.filter = state;
        },
        handleClear(){
            this.todoData = this.todoData.filter(item => item.completed == false);
        }
    },
    computed:{
        filterData() {
            switch(this.filter){
                case 'all':
                    return this.todoData;
                    break;
                case 'active':
                    return this.todoData.filter(item => item.completed == false);
                    break;
                case 'completed': 
                    return this.todoData.filter(item => item.completed == true);
                    break;
            }
        }
    },
    watch:{
        todoData:{
            deep: true,
            handler(){
                // 用数组的filter方法把todoData里completed为false的item过滤出来，其长度就是总数。
                this.total = this.todoData.filter(item => item.completed == false).length;
            }
        }
    },
    components:{
        TodoItem,
        TodoInfo
    }
}
</script>
<style scoped>
    .main-todo{
        width: 600px;
        margin: 0 auto;
        border-radius: 5px;
        overflow: hidden;
        background-color: #f9f9fc;
        box-shadow: 0 0 5px #666;
    }
    .add-todo{
        width: 100%;
        padding: 16px 16px 16px 36px;
        font-size: 24px;
        font-weight: 100;
        border: none;
        outline: none;
        box-sizing: border-box;
    }
</style>