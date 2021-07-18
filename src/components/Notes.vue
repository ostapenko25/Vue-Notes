<template>
    <!-- note list-->
    <div class="notes">
        <div class="note" :class="[ note.importance ,  {full: !grid} ]" id="notes" v-for="(note, index) in notes" :key="index">
            <div class="note-header">
                <p>{{ note.title }}</p>  
                <p class="note-remove" @click="removeNote(index)">x</p>                 
            </div>
            <div class="note-body">                   
                <span>{{ note.date }}</span>              
                <div>{{ note.descr }}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        notes: {
            type: Array, 
            required: true       
        },
        grid: {
            type: Boolean, 
            required: true
        }
    },
    methods: {
      removeNote(index) {
          console.log(`Note id${index} removed`)
          this.$emit('remove',index)//обращаемся в родительский компонент App.vue к событию по клику remove
      }
    }}
</script>
<style lang="scss">
   .notes {
       display: flex;
       align-items: center;
       justify-content: space-between;
       flex-wrap: wrap;
       padding: 40px 0
   }
   .note {
       width: 48%;
       padding: 20px;
       margin-bottom: 20px;
       background-color: #fff;     
       transition: 0.25s;

       &:hover {
        box-shadow: 0 30px 30px rgba(0,0,0,0.04);
        transform: translate(0, -6px);
       }

       &.full{
           width: 100%;         
       }

       &.high {
            background: rgb(255, 170, 148);
        }
       &.medium {
            background: rgb(255, 230, 178);
        }
       &.low {
            background: rgb(139, 186, 139)
        }

   }
   .note-body {
       p {
           margin: 20px 0;
       }
       span {
           font-size: 14px;
           color: #999
       }
   }
   .note-header {
       display: flex;
       align-items: center;
       justify-content: space-between;
       margin-top: 30px;

       h1 {
           font-size: 32px
       }

       p {
           color: blue;
           font-size: 22px
       }

       .note-remove {
           cursor: pointer;
           color: #333
       }

       svg {
           margin-right: 12px;
           color: #777;
           cursor: pointer;

           &.active {
               color: blue;
           };

           &:last-child {
               margin-right: 0
           };
           
       }
      
   }
</style>