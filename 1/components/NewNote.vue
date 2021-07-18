<template>
    <div class="new-note">
        <label>Title</label>
        <input  v-model="note.title" type="text">
        <label>Describtion</label>
        <textarea v-model="note.descr" ></textarea>
        <button class="btn btnPrimary" @click="addNote()">New Note</button>
    </div>
</template>

<script>

export default {
    props: {
        note: {
            type: Array, 
            required: true,           
        }
    },
    methods: {
        addNote() {
            this.$emit('addNote', this.note)//передать из дочернего компонента в родительский
        }
    }}
</script>

<style lang="scss">
   .new-note {
       text-align: center;
       button {
           margin-top: 20px
       }
   }
</style>