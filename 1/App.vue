<template>
  <div class="wrapper">

    <div class="wrapper-content">    

      <section>
         <div class="container">          

           <!-- error message-->
            <message v-if="message" :message="message"/>
           
             <!-- new Note-->
            <newNote 
               :note="note"
               @addNote="addNote" />

            <div class="note-header">
                <h1>{{title }}</h1>
                <div class="icons">
                    <svg :class="{ active : grid } " @click="grid = true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
                    <svg :class="{ active : !grid } " @click="grid = false" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
                </div>

             </div>

            <!-- Note list-->
            <notes 
              :notes="notes"
              @remove="removeNote"
              :grid="grid"
            />

            
         </div>
      </section>

    </div>

  </div> 
</template>

<script>
import Message from './components/Message.vue';
import newNote from './components/NewNote.vue';
import notes from './components/Notes.vue';

export default {
  components: {
    message: Message,
    newNote: newNote,
    notes: notes
  },
  data() {
    return {
    title: "Notes App",
    message: null,
    grid: true,
    note: [
      {
        title: '',
        descr: ''
      }
    ],
    notes: [
        {
          title: 'First note',
          descr: 'Descr for First note',
          date: new Date(Date.now()).toLocaleDateString()
        },
        {
          title: 'Second note',
          descr: 'Descr for Second note',
          date: new Date(Date.now()).toLocaleDateString()
      },
        {
          title: 'Second note',
          descr: 'Descr for Second note',
          date: new Date(Date.now()).toLocaleDateString()
        }
      ]    
    }
  },//data - end
  methods: {
    addNote() {                       
        let {title, descr} = this.note;//обращение ко всем переменным в data.note                  
        
        console.log("this.note.title",this.note.title)  
       
       if (this.note.title === '' || this.note.title === undefined) {
              this.message = "Title can`t be blank!";                           
              return false                           
        }            
        this.notes.push( {

            //ES5
            //title: title, // this.note.title
            //descr: descr // this.note.descr

            //ES6 - елси ключ и значение совпадают, одно можно опустить
            title, // this.note.title
            descr, // this.note.descr
            date: new Date(Date.now()).toLocaleDateString()

        });

        this.message = null;
        this.note.title = ''
        this.note.descr = ''                        
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    }
  }//methods - end
}
</script>

<style>

</style>
