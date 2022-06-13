<template>
    <div class="item" >
        <button @click="del($event,index)" :data-index="index">刪除</button>
        <input  v-model="titleInput"/>
        <button @click="addItem($event)"  >新增</button>
    </div>
</template>

<script>
    export default {
        data(){

            return {
               titleInput:''
            }

        },
        props:{
           id:Number,
           item:Object,
        },
        emits:['del','addItemHtml'],
        methods: {
            del(event,index){
                console.log(index);
                event.target.parentNode.remove();
                this.$emit('del',index);
            },
            addItem(event){
               
                //console.log(event.target.parentNode);
                event.target.parentNode.remove();
                this.$emit('addItem',{title:this.titleInput,id:this.id});
                //console.log(this.item.title);
            }
        },
    }
</script>

<style  scoped>
    .item{
        display: flex;
        justify-content: space-between;
        margin-top: 10px;
    }
    .item input{
        margin-left: 10px;
        margin-right: 10px;
    }
</style>