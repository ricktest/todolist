<template>
    <div>
        <select @change="statusChange" v-model="selected">
            <option value="2" selected>全部</option>
            <option value="0">未完成</option>
            <option value="1">已完成</option>
        </select>
    </div>
</template>

<script>
    export default {
        data(){

            return{
                selected: 2
            }
        },
        emits:['statusChange'],
        methods: {

            statusChange(){
                this.$emit('statusChange',this.selected)
            },
           
        },
    }
</script>

<style lang="scss" scoped>

</style>