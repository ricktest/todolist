<template>
    <div class="itemList">
        <ItemSingle
            v-for="(item, index) in items"
            v-bind:key="index"
            :item="item"
            :id="item.id"
            :index="index"
            :isStatus="item.status"
            :start="start"
            @updateStatus="updateStatus({id:item.id,status:item.status})"
            @delitem="delitem(item.id)"
            @edit="edit({id:item.id,title:item.title})"
            @handelStart="handelStart"
            @hadelChange="hadelChange"
        />
    </div>
</template>

<script>
    import ItemSingle from './ItemSingle.vue';
    export default {
        components: {
            ItemSingle
        },
        props:{
            items:Object,
            start:Number
        },
        emits:['delitem','updateStatus','handelStart'],
        methods: {
            delitem(id){
                
                this.$emit('delitem',id);
            },
            updateStatus(updataData){
                this.$emit('updateStatus',updataData);
            },
            edit(updataData){
                this.$emit('edit',updataData);
            },
            handelStart(index){
              
                this.$emit('handelStart',index);
            },
            hadelChange(changeData){
                this.$emit('hadelChange',changeData);
            }
        },
    }
</script>

<style scoped>

</style>