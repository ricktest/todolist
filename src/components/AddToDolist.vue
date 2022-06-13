<template>
    <div class="addContent">
        <button @click="add" >add</button>
    </div>
</template>

<script>
    export default {
       
        emits:['addItemHtml'],
        methods: {

            add(){
                
                this.$emit('addItemHtml',true)
            }

        },
    }
</script>

<style  scoped>
    .addContent{
       margin-right: 20px;
    }
</style>