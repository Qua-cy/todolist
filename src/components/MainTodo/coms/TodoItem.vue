<template>
    <div :class="['todo-item', todo.completed ? 'completed' : '']">
        <input type="checkbox" v-model="todo.completed">
        <label for="">{{todo.content}}</label>
        <span class="time">{{todo.time}}</span>
        <button @click="delItem"></button>
    </div>
</template>

<script>


export default {
    name:'TodoItem',
    props:{
        todo: Object,
    },
    methods:{
        delItem() {
            this.$emit('del',this.todo.id);
        }
    }
}
</script>

<style scoped>
    .todo-item{
        display: flex;
        justify-content: space-between;
        padding: 10px;
        border-top: 1px solid rgba(0,0,0,.3);
    }
    .todo-item label{
        flex: 1;
        max-width: 413px;
        line-height: 30px;
        transition: color 0.4s;
    }
    .todo-item.completed label{
        color: #bbb;
        text-decoration: line-through;
    }
    .todo-item .time{
        line-height: 30px;
    }
    .todo-item input{
        width: 50px;
        height: 30px;
        border: none;
        appearance: none;
        outline: none;
    }
    .todo-item input::after{
        display: block;
        width: 50px;
        height: 20px;
        margin-top: 5px;
        content: ' ';
        background: url('~images/nochecked.jpg') center center no-repeat;
        background-size: contain;
    }
    .todo-item input:checked::after{
        display: block;
        width: 50px;
        height: 20px;
        margin-top: 5px;
        content: ' ';
        background: url('~images/checked.jpg') center center no-repeat;
        background-size: contain;
    }
    .todo-item button{
        border: none;
        outline: none;
        background-color: #f9f9fc;
    }
    .todo-item:hover button::after{
        content: 'x';
        color: brown;
        font-size: 24px;
        padding: 10px;
    }
</style>