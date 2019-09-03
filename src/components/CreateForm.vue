<template>
    <div id = "input">
        <input type = "text" :value = "inputingText" @change="handleChange">
        <button @click="addInputText">add</button>
    </div>
</template>


<script>

export default {
    name: "CreateForm",
    data: function(){
        return {
            inputingText: ""
        }

    },
    methods: {
        handleChange: function(event){
            this.$emit('addHandleChange',event.target.value);
            this.inputText = event.target.value;
        },
        addInputText: function(){
            this.$emit('addHandle',this.inputText)
        }
    }
}
</script>