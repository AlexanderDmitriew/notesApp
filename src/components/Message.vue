<template>
        <div class="message">
            <div class="card">
                <p>{{ messageText }}</p>
            </div>
        </div>
</template>

<script>
export default{
    props:{
        messageText:{
            type: String,
            required: true,
        },
    }
}
</script>

<style lang="scss" scoped>

.card{
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #FEE7F1;
    min-width: 100%;
    border-radius: 0.5rem;
}

.message{
    margin-top: 1rem;
    margin-bottom: 1rem;
}

p{
    color: #E70D6B;
    margin: 1rem;
}
</style>