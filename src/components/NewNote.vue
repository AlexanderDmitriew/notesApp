<template>
    <div class="new-note">
        <label>Заголовок</label>
        <input v-model="note.title" type="text">
        <label>Заметка</label>
        <textarea v-model="note.descr"></textarea>
        <button class="btn btnPrimary" @click="addNote">Добавить запись</button>
    </div>
</template>

<script>
export default{
    props:{
        note: {
            type: Object,
            required: true
        }

    },
    methods:{
        addNote(){
            this.$emit('addNote',this.note)
        }
    }
}
</script>

<style>
.new-note{
    text-align: center;
}

.btn{
    margin: 2rem;
    
}
</style>