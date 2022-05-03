<template>
  <v-container>
    <div v-for="book in books" :key="book.isbn">
      <div @click="open(book.object)">
        <a>{{ book.name }}</a>
      </div>
      <div>{{ book.author }}</div>
      <div>{{ book.date }}</div>
    </div>

    <v-dialog v-model="shown" :key="JSON.stringify(bookParent)">
      <book-details :book="bookParent" @close="close()"></book-details>
    </v-dialog>
  </v-container>
</template>
<script>
//import Service from '../servicesDetails/index.js'
//1. Poziv na service -> https://www.anapioficeandfire.com/api/books -> PODACI (10)
//2. Premapiramo u listu objekata koje prikazujemo u mainu
//3. U v-dialog (BookDetails) saljemo podatke koji nam trebaju tamo
//4. -||- prikazujemo podatke koji nam trebaju tamo

//2. 10 - naziv, prvi autor i datum izdavanja
//autore, isbn, broj stranica, izdavača, zemlja podrijetla, broj likova
import BookDetails from "../components/BookDetails.vue";

export default {
  name: "MainCommitView",
  components: { BookDetails },
  data() {
    return {
      books: [], //lista
      shown: false,
      bookParent: null,
    };
  },
  created() {
    this.getData();
  },
  methods: {
    open(book) {
      this.bookParent = book;
      this.shown = true;
    },
    close() {
      this.shown = false;
    },
    async getData() {
      //eslint-disable-next-line
      let data = await fetch("https://www.anapioficeandfire.com/api/books");

      let response = await data.json(); //lista
      for (let book of response) {
        debugger;
        let temp = {
          object: book,
          author: book.authors[0],
          name: book.name,
          date: new Date(book.released).toLocaleDateString(),
          isbn: book.isbn,
        };
        this.books.push(temp);
      }
      //   for (let item of tempData) {
      //     debugger;
      //     console.log(item);
      //     //
      //   }
    },
  },
};
</script>
