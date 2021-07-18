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

                <!-- search-->               
                <search 
                  @search="search = $event" 
                  :value="search"  
                  placeholder="Find your note"/>

                <!-- icons controls-->
                <div class="icons">
                    <svg :class="{ active : grid } " @click="grid = true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
                    <svg :class="{ active : !grid } " @click="grid = false" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
                </div>

             </div>

            <!-- Note list-->
            <notes 
              :notes="notesFilter"
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
import Notes from './components/Notes.vue';
import Search from './components/Search.vue';

export default {
  components: {
    message: Message,
    newNote: newNote,
    notes: Notes,
    search: Search
  },
  data() {
    return {
    title: "Notes App",
    search: '',
    message: null,
    grid: true,
    note: [
      {
        title: '',
        descr: '',
        importance: ''
      }
    ],
    notes: [
        {
          title: 'First note',
          descr: 'Descr for First note',          
          date: new Date(Date.now()).toLocaleDateString(),
          importance: 'high'
        },
        {
          title: 'Second note',
          descr: 'Descr for Second note',
          date: new Date(Date.now()).toLocaleDateString(),
          importance: 'medium'
      },
        {
          title: 'Second note',
          descr: 'Descr for Second note',
          date: new Date(Date.now()).toLocaleDateString(),
          importance: 'low'
        }
      ]    
    }
  },//data - end
  computed: {
    notesFilter () {
      let array = this.notes// по какому массиву ищем
      let search = this.search //что именно ищем? по какой строке фильтруем
      if (!search) return array //если поиск пустой, то вернуть весь массив (все заметки)
      //Small
      search = search.trim().toLowerCase();//убрать проблемы и сделать лоуеркейс
      //Filter
      array = array.filter(function(item) {
        if ( item.title.toLowerCase().indexOf(search) != -1) {//если такой элемент существует
            return item//то возвращаем его
        }
      })
      //Error
      return array;
    }
  },
  methods: {
    addNote() {                       
        let {title, descr, importance} = this.note;//обращение ко всем переменным в data.note                  
        
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
            date: new Date(Date.now()).toLocaleDateString(),
            importance: importance

        });

        this.message = null;
        this.note.title = '';
        this.note.descr = '';
        this.note.importance = ''                            
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    }
  }//methods - end
}
</script>

<style>

</style>
