<template>
<div>
    <input type="text"  @input="onInput">
</div>
</template>
<script>
export default { 
    name: 'SearchBar',
    methods:{
        onInput: function(event) {
            this.$emit('termChange', event.target.value);
        }
    }
}
</script>

<style scoped>
input{
    width: 75%;
    margin-bottom: 20px;
    margin-top: 20px;
}
div{
    text-align: center;
}
</style>
