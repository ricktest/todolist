<template>
    <div class="itemContent">
         <ItemSingle
            @del="del(item.id)"
            @addItem="addItem" v-for="(item, index) in todos"
            v-bind:key="index"
            :id="item.id"
            :itemSingle="item"/>
    </div>
</template>

<script>
    import ItemSingle from './ItemSingle.vue';
    export default {
        data(){
             return {
                isDelete: false,
            }
        },
        components: {
            ItemSingle
        },

        props:{
            todos:Array
        },
        emits:['del','addItemHtml'],
        methods: {

            del(index){
               this.$emit('del',index);
            },
            addItem(itemData){
                this.$emit('addItem',itemData);
            }
        },
    }
</script>

<style  scoped>
    
</style>