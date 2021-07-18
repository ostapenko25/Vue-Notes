<template>
<div class="message">
    <p>ERROR: {{message}}</p>
</div>
</template>

<script>

export default {
    props: {
        message: {
            type: String, 
            required: true,
            default: "default" 
        }
    }
}
</script>

<style lang="scss" scoped>
.message {
    text-align: center;
}
   p {
    color: red
   }
</style>