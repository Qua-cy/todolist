<template>
    <div class="todo-info">
        <span class="total"><b>{{total}}</b> item left</span>
        <div class="tabs">
            <a :class="[state == item ? 'actived' : '']" v-for="(item, index) in states" :key="index" @click="toggleState(item)">{{item}}</a>
        </div>
        <button class="clear" @click="clearCompleted">clear completed</button>
    </div>
</template>
<script>
export default {
    name: 'TodoInfo',
    props:{
        total: Number
    },
    data(){
        return {
            states:['all', 'active', 'completed'],
            state:'all'
        }
    },
    methods:{
        toggleState(state){
            this.state = state;
            this.$emit('toggleState',state);
        },
        clearCompleted(){
            this.$emit('clearCompleted');
        }
    }

}
</script>
<style scoped>
    .todo-info{
        display: flex;
        justify-content: space-between;
        font-weight: 400;
        padding: 5px 10px;
        line-height: 30px;
        border-top: 1px solid rgba(0,0,0,.2)
    }
    .todo-info .total{
        color: brown;
    }
    .todo-info .tabs{
        display: flex;
        justify-content: space-between;
        width: 250px;
    }
    .todo-info .tabs a{
        border: 1px solid brown;
        border-radius: 5px;
        padding: 0 10px;
    }
    .todo-info .tabs a.actived{
        background-color: brown;
        color: #fff;
    }
    .todo-info .clear{
        padding: 0 10px;
        background-color: #088813;
        border-radius: 5px;
        color: #fff;
        outline: none;
        border: none;
        appearance: none;
    }
</style>