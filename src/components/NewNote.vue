<template>
    <div class="new-note">

        <h2>Title</h2>
        <input  v-model="note.title" type="text">

        <h2>Describtion</h2>
        <textarea v-model="note.descr" ></textarea>

        <h2>Importance</h2>
        <div class="importance">
            <input type="radio" id="imp-high" value="high" v-model="note.importance">
            <label for="imp-high">High</label> 
            <input type="radio" id="imp-med" value="medium" v-model="note.importance">        
            <label for="imp-med">Medium</label> 
            <input type="radio" id="imp-low" value="low" v-model="note.importance">
            <label for="imp-low">Low</label>   
        </div>

        <button class="btn btnPrimary" @click="addNote()">Add note</button>

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
           margin: 0 0 20px;
       }
   }
   .importance {
       width: 30%;
       display: flex;
       justify-content: center;
       margin: 0 auto
   }
   .high {
       background: red
   }
   .medium {
        background: yellow
   }
   .low {
        background: green
   }
</style> 