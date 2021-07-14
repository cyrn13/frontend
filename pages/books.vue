<template>
    <div>
        <NavBar />
        <EditBookModal :book="selectedBook" />
        <DeleteBookModal :book="selectedBook" @onDeleted="getAll" />
    <div class="container">
      <h1>
        Reading Book List
        <bookEntryModal class="float-right" @onAdd="getAll" />
      </h1>
      <table class="table table-bordered tabled-striped">
        <thead>
          <tr class="bg-secondary text-white">
            <th>Author</th>
            <th>Title</th>
            <th>Genre</th>
            <th>Description</th>
            <th>Status</th>
            <th>&nbsp;</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="book in books" :key="book.id">
            <td>{{book.author}}</td>
            <td>{{book.title}}</td>
            <td>{{book.genre}}</td>
            <td>{{book.description}}</td>
            <td>{{book.status}}</td>
            <td>
              <b-button @click="onEdit(book)" variant="info" size="sm">
                Edit
              </b-button>
              <b-button @click="onDelete(book)" variant="danger" size="sm">
                Delete
              </b-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      books: [],
      selectedBook: {}
    }
  },
  methods: {
    async getAll() {
      await this.$axios.get('/api/books')
      .then((res)=>{
        if(res.status==200){
          this.books = res.data
        }
      })
    },
    onEdit(selectedBook) {
      this.selectedBook = selectedBook
      this.$bvModal.show('editBookModal')
    },
    onDelete(selectedBook) {
      this.selectedBook = selectedBook
      this.$bvModal.show('deleteBookModal')
    }
  },
  created() {
    this.getAll()
  }
}
</script>