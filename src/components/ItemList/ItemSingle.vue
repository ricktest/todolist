<template>
    
        <div class="item">
            
            <button @click="delitem($event)">刪除</button>
            <div class="title ">
                <input class="input" v-model="itemSingleTitle"  v-if="type"/>
                <input class="input"  v-model="itemSingleTitle"  v-else disabled />
            </div>

            <div class="title" v-if="itemStatus==0">not ok</div>
            <div class="title" v-else >ok</div>

            <button  @click="edit()" >修改</button>
            <button  @click="updateStatus()">完成</button>
        </div>
    
</template>

<script>
    
    export default {
        data(){

            return{
                type:false,
                itemSingleTitle:'',
                itemStatus:this.item.status
            }
        },
        props:{
            item:Object,
            isStatus:Number,
            index:Number,
            id:Number,
            start:Number
        },
        emits:['delitem','updateStatus','handelStart','hadelChange'],
        methods: {
            delitem(event){
                 event.target.parentNode.remove();
               this.$emit('delitem');
            },
            updateStatus(){
               this.$emit('updateStatus');
            },

            edit(){

                if( this.type){
                    this.type =false
                    this.$emit('edit');
                }else{
                    this.type =true
                }
                
            },
            handelStart(index){
                this.$emit('handelStart',index);
            },
            handelDrop(start,index){
                 this.$emit('hadelChange',{start:start,index:index});
                //console.log(start,index);
            }
        },
       
        mounted(){
            this.itemSingleTitle = this.item.title
        },
        watch:{

            item(){
                this.itemSingleTitle = this.item.title
               
            },
            "item.status":function(){
                this.itemStatus =this.item.status
                 console.log('asda');
            }

        }
       
    } 
</script>

<style  scoped>
    .item{
        display: flex;
        justify-content: space-between;
        margin-top: 10px;
        width: 500px;
    }
    .title{
        width: 50px;
        display: inline-block;
        margin-left: 10px;
        margin-right: 10px;
    }
    .input{
        width: 100px;
    }
</style>