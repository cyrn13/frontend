<template>
    <div>

        <b-modal id="deleteBookModal" title="Book Entry" ok-title="Delete Book" @ok="onDelete" ok-variant="danger">
            Do you want to continue deleting this book? <br>
            {{book.author}} {{book.title}}
        </b-modal>

    </div>
</template>

<script>
export default {
    props: {
        book: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/books/' + this.book.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Book has been deleted.')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>