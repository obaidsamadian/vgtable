<template>
       <span @dblclick="toggleEditMode">
           <input ref="editData" class="edit" @keydown.esc="discardChanges" @keydown.enter="saveChanges"  @blur="saveChanges" type="text" v-model="passedData" v-if="editMode">
           <span v-else>{{ passedData }}</span>
       </span>
</template>

<script>
    export default {
        name: "VgtInlineEdit",
        data(){
            return{
                editMode:false,
                prevData:'',
                passedData: this.cellData
            }
        },
        props:['cell-data'],
        methods:{
            toggleEditMode(event){
                this.editMode = !this.editMode;
                this.$nextTick(() => this.$refs.editData.focus());
                this.prevData = this.passedData;
                console.log(this.prevData);
            },
            saveChanges(){
                this.editMode = false;
                this.$emit('onDataChanged',this.passedData)
            },
            discardChanges(){
                this.editMode = false;
                this.passedData = this.prevData;
            }
        }
    }
</script>

<style scoped>
    input{
        height: 100%;
        width: 100%;
        border: 0;
        /* display: inline-block; */
        margin: 0px;
        position: absolute;
        top: 0;
        padding: 0px;
        left: 0px;
        font-size: 16px;
        box-sizing: border-box;
        padding: 10px;
    }
</style>