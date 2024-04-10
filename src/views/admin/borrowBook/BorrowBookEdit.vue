<template>
  <div>
    <h2>Edit Borrow Book</h2>
    <BorrowBookForm :borrowBook="borrowBook" @submit="editBorrowBook" />
  </div>
</template>

<script>
import BorrowBookForm from "@/components/admin/borrowBook/BorrowBookForm.vue";
import BorrowBookService from "@/services/borrowBook.service";

export default {
  components: {
    BorrowBookForm
  },
  props: {
    id: { type: String, required: true }
  },
  data() {
    return {
      borrowBook: null
    };
  },
  methods: {
    async editBorrowBook(data) {
      try {
        await BorrowBookService.update(this.id, data);
        alert("Borrow Book updated successfully");
        this.$router.push("/borrow-books");
      } catch (error) {
        console.error(error);
      }
    },
    async fetchBorrowBook() {
      try {
        this.borrowBook = await BorrowBookService.getById(this.id);
      } catch (error) {
        console.error(error);
      }
    }
  },
  created() {
    this.fetchBorrowBook();
  }
};
</script>
