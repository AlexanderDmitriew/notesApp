<template>
  <div class="wrapper">
  
    <div class="wrapper-content">
      <section>
        <div class="container">
          <div class="header">
        </div>
        <!-- Сообщение об ошибке -->
          <message v-if="messageText" :messageText=messageText />

        <!-- new note -->
          <newNote :note = "note" @addNote="addNote"/>

          <!-- title -->
          <div class="note_header">
            
            <h1 class="ms-2">{{ title }}</h1>
            <!-- Поиск -->
            
            <search 
            :value="search" 
            placeholder="Find your note" 
            @search="search = $event"/>
            
            <div class="icons">
              <svg :class="{active: grid}" @click="grid = true" style="cursor:pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
              <svg :class="{active: !grid}" @click="grid = false" style="cursor:pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
          </div>

        <!-- notes list -->
          <notes :notes="notesFilter" :grid="grid" @remove="removeNote"/>

        </div>
      </section>
    </div>

  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from "@/components/Notes.vue"
import search from "@/components/Search.vue"

export default {
  components:{
    message,
    newNote,
    notes,
    search
  }, 
  data(){
    return{
      title: "Notes App",
      search: '',
      messageText: null,
      grid: true,
      note: {
        title: '',
        descr: '',
      },
      notes: [
      {
        title: 'First Note',
        descr: 'Description for first note',
        date: new Date(Date.now()).toLocaleString()
      },
      {
        title: 'Second Note',
        descr: 'Description for second note',
        date: new Date(Date.now()).toLocaleString()
      },
      {
        title: 'Third Note',
        descr: 'Description for third note',
        date: new Date(Date.now()).toLocaleString()
        }
      ]
    }
  },
  methods: {
    addNote() {
        let { title, descr } = this.note
        if (title === '') {
          this.messageText = 'Заголовок не может быть пустым'
          return false
        }
        this.notes.push({
          title,
          descr,
          date: new Date(Date.now()).toLocaleString()
        })
        this.note.title = ''
        this.note.descr = ''
        this.messageText = null
      },

      // Удаление записи
      removeNote(index){
        this.notes.splice(index, 1)
      }
    },
    computed:{
      notesFilter(){
        let array = this.notes,
        search = this.search
        if(!search) return array
        //lowercase
        search = search.trim().toLocaleLowerCase()
        //Filter
        array = array.filter(function(item){
          if(item.title.toLocaleLowerCase().indexOf(search) !== -1){
            return item
          }
        })
        //Error
        return array
      }
    }
}
</script>

<style scoped>
.header{
  display: flex;
}

.ms-2{
  margin-left: 0.5rem
}
</style>
