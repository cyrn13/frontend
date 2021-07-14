<template>
    <div>
        

        <b-modal id="editBookModal" title="Book Entry" ok-title="Save Book" @ok="onSubmit">
            <form action="#" >
                <b-form-group
                    label="Author"
                    label-for="author"   
                >
                    <b-form-input id="author" v-model="book.author"  trim></b-form-input>
                    </b-form-group>

                    <b-form-group
                    label="Title"
                    label-for="title"     
                >
                    <b-form-input id="title" v-model="book.title"  trim></b-form-input>
                    </b-form-group>

                    <b-form-group
                    label="Genre"
                    label-for="genre" 
                >
                    <b-form-select v-model="book.genre" :options="genres"></b-form-select>
                    </b-form-group>

                    <b-form-group
                    label="Description"
                    label-for="description"
                >
                    <b-form-input id="description" v-model="book.description"  trim></b-form-input>
                    </b-form-group>

                    <b-form-group
                    label="Status"
                    label-for="status"
                >
                    <b-form-select v-model="book.status" :options="status"></b-form-select>
                    </b-form-group>

            </form>
        </b-modal>

    </div>
</template>

<script>
export default {
  props: {
      book: {}
  },
  data() {
      return {
           status: [
                {value: 'current', text: 'Currently reading.'},
                {value: 'done', text: 'Finished reading.'},
                {value: 'not yet', text: 'Have not read it yet.'},
            ],

            genres: [
                {value: 'Fiction', text: 'Fiction'},
                {value: 'Narrative', text: 'Narrative'},
                {value: 'Novel', text: 'Novel'},
                {value: 'Non-fic', text: 'Non-Fiction'},
                {value: 'Sci-fi', text: 'Science Fiction'},
                {value: 'Mystery', text: 'Mystery'},
                {value: 'His-fi', text: 'History Fiction'},
                {value: 'Horror', text: 'Horror Fiction'},
                {value: 'Fantasy', text:'Fantasy'},
                {value: 'Thriller', text: 'Thriller'},
                {value: 'Poetry', text: 'Poetry'},
                {value: 'Romance', text: 'Romance Novel'}
            ]
      }
  },
  methods: {
      async onSubmit(){
          this.$axios.put('/api/books/' + this.book.id, this.book)
          .then((res)=>{
              if(res.status==202) {
                  alert('Updated successfully!')
              }
          })
          .catch((err)=>{
              alert(err.message)
          })
      }
  }
    
}
</script>