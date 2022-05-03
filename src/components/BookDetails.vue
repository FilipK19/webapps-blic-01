<template>
  <v-card>
    <v-card-title>Book details</v-card-title>
    <v-card-text>
      <div>Author: {{ book.authors[0] }}</div>
      <div>ISBN: {{ book.isbn }}</div>
      <div>Page count: {{ book.numberOfPages }}</div>
      <div>Number of characters: {{ book.characters.length }}</div>
    </v-card-text>
    <v-card-actions @click.stop="$emit('close')"> BACK </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "BookDetails",
  props: ["book"],
  data() {
    return {};
  },
  created() {
    debugger;
  },
};
</script>
