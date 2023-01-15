<template>
    <div class="notes">
        <div class="note" :class="{full: !grid}" v-for="(note, index) in notes" :key="index">
            <div class="note_header" :class="{full: !grid}">
                <p>{{note.title}}</p>
                <p style="cursor: pointer;" @click="removeNote(index)">x</p>
            </div>
            <div class="note-body">
                <p>{{note.descr}}</p>
                <span>{{note.date}}</span>
            </div>
            <hr>
        </div>
    </div>
</template>

<script>
export default{
    props:{
        notes:{
            type: Array,
            required: true
        },
        grid:{
            type: Boolean,
            required: true
        }
    },
    methods:{
        // удаление записи по index 
        removeNote(index){
            console.log(`Note id - ${index} removed`)
            this.$emit('remove', index)
        }
    }
}
</script>

<style lang="scss">
.notes{
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 4rem, 0;
    margin-top: 2rem;
}

.note{
    width: 40%;
    padding: 2rem;
    margin-bottom: 1.5rem;
    background-color: #fff;
    transition: all cubic-bezier(.02, .01, .47, 1);
    box-shadow: 0 30px 30px rgba(0,0,0,.02);
    &:hover{
        box-shadow: 0 30px 30px rgba(0,0,0, .04);
        transform: translate(0, -6px);
        transition-delay: 0s !important;
    }
    &.full{
        width: 100%;
        text-align: center;
    }
}

.note_header{
    display: flex;
    align-items: center;
    justify-content: space-between;
    p{
        font-size: 22px;
        color: #402caf;
    }
    svg{ 
        margin-right: 0.7rem;
        color: #999;
        &.active{
            color:#402caf;
        }
        &:last-child{
            margin-right: 0;
        }
    }
    &.full{
        justify-content: center;
        P{
            margin-right: 16px;
            &:last-child{
                margin-right: 0;
            }
        }
    }
}
</style>