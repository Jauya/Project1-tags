<script>
    export default{
        emits: ["onTagsChange"],
        data(){
            return {
                currentValue: "",
                tags: [],
            };
        },

        methods: {
            handleSubmit(){
                if(this.currentValue !== ""){
                    const exist = this.tags.some(item => item == this.currentValue)
                    if(!exist){
                        this.tags.push(this.currentValue);
                        this.currentValue = "";
                        this.$emit('onTagsChange',this.tags);
                    }
                }
            },
            handleDelete(e){
                if(this.currentValue == "" && e.key == "Backspace"){
                    this.tags.pop();
                    this.$emit('onTagsChange',this.tags);
                }
            },
            deleteTag(tag){
                this.tags = this.tags.filter((item) => item !== tag);
                this.$emit('onTagsChange',this.tags);
            }
        },
    }
</script>

<template>
    <div class="container">
        <h1>Entrada de tags</h1>
        <div class="inputTag">
            <div class="tags">
                <div class="tag" v-for="(tag,index) in tags" :key="index">
                    {{ tag }}<button @click="deleteTag(tag)">X</button>
                </div>
            </div>
            <form @submit.prevent="handleSubmit">
                <input class="input" type="text" v-model="currentValue" @keydown="handleDelete"/>
            </form>
        </div>
    </div>
</template>

<style scoped>
    .container{
        height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: rgb(39, 39, 39);
        padding-inline: 10px;
        color: rgb(172, 170, 168);
    }
    .inputTag{
        display: inline-flex;
        border: 2px solid rgb(77, 77, 77);
        border-radius: 3px;
        height: 45px;
        min-width: 300px;
        max-width: 600px;
        overflow-x: auto;
        overflow-y: hidden;
        background-color: rgb(68, 68, 68);
    }
    .inputTag::-webkit-scrollbar{
        height: 5px;
        background-color: inherit;
        border-radius: 5px;
    }
    .inputTag::-webkit-scrollbar-thumb{
        background-color: rgb(128, 128, 128);
        border-radius: 5px;
    }
    .tags{
        display: flex;
        gap:3px;
        padding: 5px;
    }
    .tag{
        width: max-content;
    }
    .tags .tag{
        display: flex;
        padding: 5px;
        border: solid 1px rgb(148, 148, 148);
        border-radius: 5px;
        align-items: center;
    }
    .inputTag form{
        display: inline-flex;
    }
    .input{
        background-color: inherit;
    }
    .inputTag form::before{
        content: ">";
        color: rgb(117, 117, 117);
        display: flex;
        align-self: center;
        font-size: 20px;
        font-weight: 100;
    }
    .inputTag .input{
        border: none;
        outline: none;
        padding: 0 5px;
        font-size: 17px;
        color: rgb(199, 199, 199);
    }
    .inputTag button{
        background-color: transparent;
        border: none;
        cursor: pointer;
        color: rgb(139, 139, 139);
    }
</style>
